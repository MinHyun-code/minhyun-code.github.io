---
layout: post
title: "공통코드 관리 방법"
subtitle: "study"
category: "java"
date: 2024-07-30
background: '/img/posts/common code.png'
---

## Enum vs DB

공통코드를 관리하는 방법은 Java `Enum`을 사용하거나 `DB`에 저장하는 방법이 있다.

변경 빈도 수가 잦으면 `DB`, 빈도 수가 거의 없다하면 `Enum`을 선택하면 된다.

<br>

## Enum 

이 게시글은 Enum을 사용하는 방법을 위한 것으로, DB는 따로 다루지 않을 것이다.

<br>

**대부분 코드는 코드 값, 코드 명, 코드 옵션으로 셋팅되어 있어 인터페이스를 먼저 생성한다.**

```java
public interface CommCode {

  String getCode();

  String getName();

  String getOption();
}
```

<br>
<br>

**만들어놓은 인터페이스를 implements한 후 리턴 값을 enum으로 셋팅**

```java
@JsonFormat(shape = JsonFormat.Shape.OBJECT)
@Schema(description = "복지혜택 신청 상태 01:대기, 02:승인(입금예정), 03:입금완료, 04:반려, 05:입금완료(미사용 코드), 06:삭제, 07:수정")
public enum WelfareStatus implements CommCode {
  
    @JsonProperty("01")
    WAIT("01", "대기", ""),
    @JsonProperty("02")
    SCHEDULE("02", "승인(입금예정)", ""),
    @JsonProperty("03")
    COMPLETE("03", "입금완료", ""),
    @JsonProperty("04")
    REJECT("04", "반려", ""),
    @JsonProperty("05")
    ACCEPT("05", "입금완료(미사용 코드)", ""),
    @JsonProperty("06")
    DELETE("06", "삭제", ""),
    @JsonProperty("07")
    UPDATE("07", "수정", ""),
    
    ;

    private static final Map<String, String> CODE_MAP = Collections.unmodifiableMap(Stream.of(values()).collect(Collectors.toMap(WelfareStatus::getCode, WelfareStatus::name)));
    @Getter
    private static final Map<String, String> CODE_MAP_NM = Collections.unmodifiableMap(Stream.of(values()).collect(Collectors.toMap(WelfareStatus::getCode, WelfareStatus::getName)));

    @Getter
    private final String code;
    @Getter
    private final String name;
    @Getter
    private final String option;

    WelfareStatus(String code, String name, String option) {
        this.code = code;
        this.name = name;
        this.option = option;
    }

    @MappedTypes(WelfareStatus.class)
    public static class TypeHandler extends CommCodeEnumTypeHandler<WelfareStatus> {
        public TypeHandler() {
            super(WelfareStatus.class);
        }
    }

    public static WelfareStatus of(final String code) {
        return valueOf(CODE_MAP.get(code));
    }

    @JsonCreator
    public static WelfareStatus from(final String welfareStatus) {
        return WelfareStatus.of(welfareStatus);
    }
    
    public static Map<String, String> codeName() {
        return CODE_MAP_NM;
      }
}

```

<br>

@Schema : Swagger UI에서 보여질 내용

@JsonFormat(shape = JsonFormat.Shape.OBJECT) : Front json 값 전달시 enum 객체 자체를 전달하여 front에서 code, name을 직접 선택하여 사용할수 있도록 한다.

@JsonProperty : key를 매핑시키는 역할


<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://velog.io/@woosim34/Enum-%ED%99%9C%EC%9A%A9%EA%B3%B5%ED%86%B5%EC%BD%94%EB%93%9C%EB%A5%BC-Enum%EC%9C%BC%EB%A1%9C>
<div>
