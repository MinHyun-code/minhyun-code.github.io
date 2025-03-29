---
layout: post
title: "Mail 전송 - 템플릿 적용 방법"
subtitle: "EMAIL"
category: "java"
date: 2024-01-22
background: '/img/posts/mailSendTemplate.png'
---


> 기존에 메일 전송은 구현한 경험이 있으므로, 
> 
> 템플릿을 적용하는 방법만 정리하였습니다. 
>

<br>
<br>

# Mail 전송 - 템플릿 적용 방법

1 . `.template` 파일 저장 (html 파일) - 값이 적용될 부분에 `$변수 명$` 입력

<br>

2 . 해당 template 파일을 읽어 String 변수에 저장

```java
// java8
    Path fileName = Path.of("src/main/resources/template/test.txt");
    String fileData = Files.readString(fileName);


// java 11
    Path filePath = Paths.get("src/main/resources/template/test.txt");

    List<String> lines = Files.readAllLines(filePath);
    String fileData = "";
    for (String line : lines) {
        fileData += line;
    }
```
<br>

3 . fileData의 데이터 중 `$변수 명$`에 값 replace

<br>

4 . 태그 변환

```java
        Map<String, String> guideMap = new HashMap<String, String>();
        guideMap.put("&lt;", "<");
        guideMap.put("&gt;", ">");
        guideMap.put("&#39;", "'");

        for(String ch : guideMap.keySet()) {
            value = value.replaceAll(ch, guideMap.get(ch));
        }
```

<br>

5 . 메일 전송

```java
    MimeMessage msg = mailSender.createMimeMessage();
    MimeMessageHelper helper = new MimeMessageHelper(msg, false);
    helper.setText(fileData, true); 
```

<br>


<br>
<br>
<br> 


