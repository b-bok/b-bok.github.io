---
title: jackson 어노테이션
date: 2021-02-24 23:02:48
category: spring
draft: false
---

#### 오늘 학습한 내용

#### Jackson annotation

-> 직렬화는 자바를 json 형태로 변경하는 것을 의미합니다. 즉 객체를 전송 가능한 혀태로 바꿔주는 것을 의미합니다. 역직렬화란 데이터를 다시 자바 객체로 변환해주는 것을 의미합니다.

https://pjh3749.tistory.com/281

참고로, 접근 제한자가 public인 것들은(직렬화, 역직렬화 할때 필요)getter setter를 넣으면 코드가 길어지고, Lombok을쓰면 Jackson 어노테이션과 혼동 될 수 있기때문에!

## 직렬화

### @jsonAnyGetter

​ jsonAnyGetter는 Map 필드를 다루는데 유연성을 제공합니다. Member 클래스가 Map으로 속성을 가지고 있을 경우

```java
public class Member {
  public String name;
  private Map<String, String> properties;

  public Member(String name) {
      this.name = name;
  }

  @JsonAnyGetter
  public Map<String, String> getProperties() {
      return propeties;
  }

  public void add(String attr, String val) {
      this.properteis.put(attr, val);
  }
}
```

```java
@Test
public void json_any_getter() throws JsonProcessingException {
    Member member = new Member("Jay");
    member.add("favorite", "chicken");
    member.add("hobby", "tennis");
    String result = new ObjectMapper().writeValueAsString(member);
    assertThat(result, containsString("favorite"));
    assertThat(result, containsString("hobby"));
}

// 결과는?

{"name":"Jay","favorite":"chicken","hobby":"tennis"}

//만약 @JsonAnyGetter 어노테이션이 없으면?
{"name":"Jay","properties":{"favorite":"chicken","hobby":"tennis"}}
// 필요 상황에 맞게 커스텀 가능!
```

Map 타입이 전부 key-value 형식으로 json에 들어있는 것을 볼 수 있다!

### @JsonGetter

@JsonGetter는 메서드 이름을 getter메서드로 표현하기 위해 @JsonProperty 어노테이션의 대안

```java
public class Member2 {
    public int id;
    private String name;

    public Member2(int id, String name) {
        this.id = id; this.name = name;
    }

    @JsonGetter("name")
    public String getTheName() {
        return name;
    }
}


// setter는?
@JsonSetter("name")
public void setTheName(String name) {
    this.name = name;
}

```

@JsonGetter의 이름으로 name을 썼음 => name 필드를 get 하는 것이다!

```java
@Test
public void json_getter() throws JsonProcessingException {
	Member2 member = new Member2(1, "Jay");
    String result = new ObjectMapper().writeValueAsString(member);
    assertThat(result, containsString("Jay"));
    assertThat(result, containsString("1"));
}
```

### @JsonPropertyOrder

@JsonPropertyOrder를 통해서 직렬화 하는 속성의 순서를 정한다!

```java
@JsonPropertyOrder({ "name", "id" })
    public class Member3 {
    public int id;
    public String name;
    public Member3(int id, String name) {
    this.id = id; this.name = name;
    }
}

// 출력했을때 순서가
{"name":"My bean","id":1}
// @JsonPropertyOrder가 없다면
// id - name 순서로!


```

### @JsonValue

@JsonValue는 전체 인스턴스를 직렬화 할때 사용하는 단일 메서드// 예를 들어 enum에서 getName 메서드에 @JsonValue를 넣어주어 이름을 통해 직렬화 즉, 아래 같은 상황에서 @JsonValue 없이 직렬화를 하면 TYPE1이 나오지만, @JsonValue를 넣게 되면 치킨이 나온다!

```java
public enum TypeEnumWithValue {
    TYPE1(1, "치킨"),
    TYPE2(2, "피자");

    private Integer id;
    private String name;
    TypeEnumWithValue(Integer id, String name) {
    this.id = id; this.name = name;
    }
    @JsonValue
    public String getName() {
    return name;
    }
}

new ObjectMapper().writeValueAsString(TypeEnumWithValue.TYPE1);

//-> 결과가 치킨, 피자

```

### @JsonRootName

@JsonRootName 어노테이션은 root wrapper의 이름 설정 가능!

```java
{ "id": 1, "name":"Jay" } { "Member": { "id": 1, "name": "Jay" }
```

```java
@JsonRootName(value = "member")
public class Member4 {
    public int id;
    public String name;

    public Member4(int id, String name) {
    this.id = id;
    this.name = name;
    }
}
```

JsonRootName을 member로 지정하면 wrapping된 결괄를 얻을 수 있다!

```java
@Test
public void json_root_name() throws JsonProcessingException {
    Member4 user = new Member4(1, "Jay");
    ObjectMapper mapper = new ObjectMapper(); 			                         mapper.enable(SerializationFeature.WRAP_ROOT_VALUE); // ObjectMapper 설정 변경해줘야함!
    String result = mapper.writeValueAsString(user);
    System.out.println(result);
    assertThat(result, containsString("Jay"));
    assertThat(result, containsString("member"));
}


```

### @JsonSerialize

@JsonSerialize는 엔티티를 marshalling 할 때 사용자가 지정한 커스텀 serializer를 쓸 수 있게 해줍니다. 직렬화를 사용자가 커스텀 할때 StdSerializer를 이용해서 구현합니다.

StdSerializer를 상속받아 커스텀한 클래스!

```java
public class CustomDateSerializer extends StdSerializer<Date> {
    private static SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy hh:mm:ss");

    public CustomDateSerializer() {
    	this(null);
    }
    public CustomDateSerializer(Class<Date> t) {
    	super(t);
    }

    @Override
    public void serialize(Date value, JsonGenerator gen, SerializerProvider arg2) throws IOException {

    	gen.writeString(formatter.format(value));

    }
}
```

```java
@Test
public void json_serialize() throws ParseException, JsonProcessingException {

    SimpleDateFormat df = new SimpleDateFormat("dd-MM-yyyy hh:mm:ss");
    String toParse = "20-12-2014 02:30:00";
    Date date = df.parse(toParse);
    Event event = new Event("party", date);
    String result = new ObjectMapper().writeValueAsString(event);
    assertThat(result, containsString(toParse));
}
```

다음 처럼 객체 필드의 포맷을 변경하지 않고, 직렬화시 변경해주고 싶은 필드만 변경가능!

## 역직렬화

### @JsonCreator

@JsonCreator를 이용해서 역직렬화 할때 생성자나 팩토리 수정 가능

```
{ "id":1, "theName":"Jay" }
```

theName이라는 필드를 쓰기 싫다면!

```java
public class Member5 {
    public int id;
    public String name;

    @JsonCreator
    public Member5(@JsonProperty("id") int id, @JsonProperty("theName") String name) { this.id = id;
    this.name = name;
    }
}

```

@JsonCreator랑 @JsonProerty를 사용하면 해결!

### @JacksonInject

@JacksonInject는 json 데이터가 아닌 곳에서 값을 주입할 때 사용합니다.

```java
public class Member6 {
    @JacksonInject
    public int id;
    public String name;
}


@Test
public void json_inject() throws JsonProcessingException {
    String json = "{\"name\":\"Jay\"}";
    InjectableValues injectableValues = new InjectableValues.Std().addValue(int.class, 5); Member6 member = new ObjectMapper().reader(injectableValues).forType(Member6.class).readValue(json); assertThat(member.id, is(5));
}

```

### @JsonAnySetter

@JsonAnySetter는 Map을 다룰 때 유용하다!

```java
public class Member7 {

    public String name;
    public Map<String, String> properties = new HashMap<>();
    @JsonAnySetter
    public void add(String key, String value) {
    properties.put(key, value);
	}
}

@Test public void json_any_setter() throws IOException {

    String json = "{\"name\":\"Jay\",\"favorite\":\"chicken\",\"hobby\":\"tennis\"}";
    Member7 member = new ObjectMapper().readerFor(Member7.class).readValue(json); assertThat(member.properties.get("favorite"), is("chicken"));

}

```

### @JsonDeserialize

커스텀으로 역직렬화를 만들 수 있다! JsonDeserializer가 StdDeserializer의 상위 클래스로 상속받아서 만들어도 된다!

```java
public class CustomDateDeserializer extends StdDeserializer<Date> {
private static SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy hh:mm:ss"); public CustomDateDeserializer() { this(null);
}

public CustomDateDeserializer(Class<?> vc) {
super(vc);
}

@Override
public Date deserialize(JsonParser parser, DeserializationContext ctxt) throws IOException {
        String date = parser.getText();
        try {
        return formatter.parse(date);
        }
        catch (ParseException e) {
        throw new RuntimeException(e);
        }
	}
}


@Test
public void json_deserializer() throws JsonProcessingException {
    String json = "{\"name\":\"Jay event\",\"eventDate\":\"20-12-2020 01:01:00\"}"; SimpleDateFormat df = new SimpleDateFormat("dd-MM-yyyy hh:mm:ss");
    Event2 event = new ObjectMapper()
        			.readerFor(Event2.class)
        			.readValue(json);

    assertThat(df.format(event.eventDate), is("20-12-2020 01:01:00"));
}


```

### @JsonAlias

@JsonAlias는 역직렬화를 할 때 한 개 이상의 이름을 한 객체 필드에 매핑되게 설정 할 수 있다.

```java
public class Member8 {
    @JsonAlias({"name", "his_name", "her_name"})
    public String name;
    public String hobby;
}
```

```java
@Test
public void json_alias() throws JsonProcessingException {
String json1 = "{\"name\":\"Jay\",\"hobby\":\"tennis\"}";
String json2 = "{\"his_name\":\"Jay\",\"hobby\":\"tennis\"}";
String json3 = "{\"her_name\":\"Jay\",\"hobby\":\"tennis\"}";
Member8 member1 = new ObjectMapper().readerFor(Member8.class).readValue(json1);
Member8 member2 = new ObjectMapper().readerFor(Member8.class).readValue(json2);
Member8 member3 = new ObjectMapper().readerFor(Member8.class).readValue(json3);

assertThat(member1.name, is("Jay"));
assertThat(member2.name, is("Jay"));
assertThat(member3.name, is("Jay"));

}
// name, his_name, her_name 중 어떤 것으로 들어오든 name으로 매핑 가능!
```

## Jackson Property Inclusion Annotations

### @JsonIgnoreProperties

@JsonIgnoreProperties 어노테이션은 클래스 레벨에 붙는 어노테이션

Jackson이 무시할 필드를 설정 할 수 있다.

```java
@JsonIgnoreProperties({"id"})
public class Member9 {
    public int id;
    public String name;
    public Member9(int id, String name) {
    this.id = id;
    this.name = name;
    }
}

@Test
public void json_ignore_properties() throws JsonProcessingException {
    Member9 member = new Member9(1, "Jay");
    String result = new ObjectMapper().writeValueAsString(member);
    assertThat(result, containsString("Jay"));
    assertThat(result, not(containsString("1")));
}

```

id 필드를 직렬화시 제외시킨후 결과가 나옵니다! 클래스 레벨이 아닌 필드레벨에서 쓰고 싶다면 @JsonIgnore를 사용하면 됩니다! 클래스 전부를 제외하고 싶다면 @JsonIgnoreType를 씁니다.

```java
@JsonIgnore
public int id;
public String name;

// 클래스 내부
@JsonIgnoreType
public static class Name {
    public String firstName;
    public String lastName;
}
```

### @JsonInclude

@JsonInclude Non_NuLL 은 null을 직렬화시 제거합니다.

```java
@JsonInclude(JsonInclude.Include.NON_NULL)
    public class Member10 {
    public int id;
    public String name;
    public Member10(int id, String name) {
    	this.id = id;
    	this.name = name;
    }
}

@Test
public void json_include() throws JsonProcessingException {
Member10 member = new Member10(1, null);
String result = new ObjectMapper().writeValueAsString(member);
assertThat(result, containsString("1"));
assertThat(result, not(containsString("name")));
}

```

### @JsonAutoDetect

@JsonAutoDetect를 이용해 필드 직렬화 대상을 정할 수 있습니다. 이번에는 접근제한자를 잘 봐야합니다.

JsonAutoDetect의 가시성 범위는 ANY, NON_PRIVATE, PROTECTED_AND_PUBLIC 등등 여러 속성이 있으니 필요한 것들을 골라 쓰면 될 것 같습니다.

현재 접근 제한자가 id와 name은 접근 제한자가 private입니다 그래서 @JsonAutoDetect로 가시 범위를 설정합니다. ANY는 private 필드까지 모두 직렬화 접근이 가능합니다.

```
@JsonAutoDetect(fieldVisibility = JsonAutoDetect.Visibility.ANY)
public class Member11 {
    private int id;
    private String name;

	public Member11(int id, String name) {
    this.id = id;
    this.name = name;
    }
}


```

### @JsonProperty

직렬화시 설정할 수 있는 이름을 지정하는 어노테이션 입니다.

```
private String name;

@JsonProperty("name")
public void setTheName(String name) {
    this.name = name;
}

@JsonProperty("name")
public String getTheName() {
	return name;
}


```

출처: https://pjh3749.tistory.com/281 [JayTech의 기술 블로그]
