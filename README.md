# JAVA_study2

회사 일 경험 3개월 인턴 학습 일지

# 2일 ~ 4일차
첫번째 간단한 JSP, Javascript을 활용한 회원가입 만들기 과제
<br>
두번째 Jquery, javascript 활용한 체크박스


## 과제 회원가입조건
id : 문자(영어), 숫자만, 중복체크, "test" 
<br>
pw : 비밀번호확인(가입신청버튼 클릭시)  
<br>
이름 : 5글자(maxlength x)-script <br>
        문자(한글,영어)<br>
        5글자 넘어갈 시 바로 체크<br>
<br>
이메일 : 유효성(가입신청버튼 클릭시)
<br>
휴대폰 : 숫자만 4자리 -> 3번째로 4개 입력하면 3번째 창으로 커서이동
<br>
주민번호 : 숫자만 주민번호 유효성 뒷자리 맨첫자리만 숫자 1****** <br>
	 (가입 신청클릭시)


## 과제 코딩
index.JSP

<details>
    <summary>코드 보기</summary>
	
```jsp

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script defer type="text/javascript" src=/js/reply.js></script>
<link rel="stylesheet" href="css/index.css">
<script defer src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<title>회원가입</title>


</head>
<body>
<form name="frm">

<input type="hidden" name="jumi">

		<tr>
		<br>
			<td>회원가입</td>
		<br><br>
		</tr>
		
		<hr><br>
		
		<div>
		<br><br>
			ID :
			<input type="text" id="id" name="userid" maxlength="15" size="10">
			<input type="button" name = "idChk" value="중복체크" onclick="idCheck()">
			<br>
			비밀번호 :
			<input type="password" id="pwd" name="pwd" maxlength="20" size="15">
			<br>
			비밀번호확인 :
			<input type="password" id="pwd2" name="pwd2" maxlength="20" size="15">
			<br>
			이름 :
			<input type="text" id="name" name="name" onkeyup="checkName()">
			<br>
			이메일 :
			<input type="email" id="email1" name="email1" size="15" maxlength="10">@<input type="email" id="email2" name="email2" size="15" maxlength="12">
			<br>
			핸드폰 :
			<select name="s">
				<option value="010">010</option>
				<option value="011">011</option>
				<option value="016">016</option>
				<option value="017">017</option>
				<option value="019">019</option>
			</select>
			- <input type="text" id="ph1" name="ph1" maxlength="4" size="10" onkeyup="phone()">
			- <input type="password" id="ph2" name="ph2" maxlength="4" size="10">
			<br>
			
			성별 :
			<input type="radio" id="man" name="gender">남자
			<input type="radio" id="woman" name="gender">여자
			<br>
			주민번호 :
			<input type="text" id="mm1" name="mm1" maxlength="6" onkeyup="checkmm()">
			-<input type="text" id="mm2" name="mm2" maxlength="7">
			
			<br>
			
			주소 :
			<input type="text" id="url" name="url">
			<br>
			*주소는 (시/도)만 입력해주세요 (예: 경기도, 서울특별시, 경상남도 등)
		</div>
		<hr>
		
		<div class="centers">
			<tr>
			<input type="button" value="가입신청" onclick="checkform()">
			<input type="reset" value="다시입력">
			<input type="button" value="취소">
			</tr>
		</div>
	
</form>

</body>
</html>

```
</details>

<br>
<br>

reply.js
<br>

<details>
    <summary>코드 보기</summary>
	
```javascript



function phone(){
	let ph1 = document.frm.ph1.value;
	// 핸드폰 확인
    if(ph1.length == 4){
    	alert(ph1.length);
    	document.frm.ph2.focus();
    }
	
}


function checkName(){
   
    	const regex = /^[가-힣a-zA-Z]+$/;
    	let name = document.frm.name.value;
    	
    	
    	if(name.length > 5){
    		alert("이름은 최대 5글자입니다");
    		name = name.substring(0,5);
    	}else if(!regex.test(name)){
    		alert("한글 또는 영어로만 입력이 가능합니다");
    		document.frm.name.focus();
    	}
    }

function checkmm(){
	// 주민번호 확인
	
    if(document.frm.mm1.value.length == 6){
    	document.frm.mm2.focus();
    }
   
}



// 아이디 중복 체크
function idCheck(){
	
	const id = document.frm.userid.value;
	
	if("" == id){
		alert("아이디를 입력하세요.");
	}else if("koyu123" == id){
		alert("아이디가 중복되었습니다");
	}else if(id.length < 4){
		alert("아이디가 너무 짧습니다");
	}else {
		alert("아이디 사용이 가능합니다");
	}
}

function isValidJumin(jumin) {
 

    // 주민등록번호의 각 자리수
    const digits = jumin.split('').map(Number);

    // 가중치 배열
    const weights = [2, 3, 4, 5, 6, 7, 8, 9, 2, 3, 4, 5];

    // 체크 디지트 계산
    let sum = 0;
    for (let i = 0; i < 12; i++) {
        sum += digits[i] * weights[i];
    }
    const checkDigit = (11 - (sum % 11)) % 10;
   
   
    // 실제 체크 디지트와 비교
    return checkDigit == digits[12];
   
   
}

 function checkform(){
	const id = /^[a-zA-Z0-9]*$/;

	let user = document.frm.userid.value;
	let userpwd1 = document.frm.pwd.value;
	let userpwd2 = document.frm.pwd2.value;
	
	let email1 = document.frm.email1.value;
	let email2 = document.frm.email2.value;
	
	const email = email1 + "@" + email2;
	const email_pattern = /^[A-Za-z0-9_\.\-]+@[A-Za-z0-9\-]+\.[A-za-z0-9\-]+/;
	
	
	// 아이디 글자 확인
	if(user == ""){
		alert("아이디를 입력해주세요");
		document.frm.userid.focus();
        return false;
	}else if(userpwd1 == ""){
		alert("비밀번호를 입력해주세요");
		document.frm.pwd.focus();
        return false;
	}else if(userpwd2 == ""){
		alert("비밀번호확인을 입력해주세요");
		document.frm.pwd2.focus();
        return false;
	}else if(!(id.test(user))){
		alert("한글은 입력하면 안됩니다.");
		document.frm.userid.focus();
        return false;
	}
	
	
	
	// 비밀번호 확인
	if(userpwd1 !== userpwd2){
        alert("비밀번호와 동일하지 않습니다.")
        document.frm.pwd2.focus();
        return false;
    }
	// 이메일 유효성
    if(!email_pattern.test(email)){
    	alert("유효한 이메일 정보를 입력하시길 바랍니다");
    }
	
    let mm1 = document.frm.mm1.value;
    let mm2 = document.frm.mm2.value;
   
   
    let number = /^\d{13}$/;

		
	let maskJumin ="";
	let jumins = mm2;
	let jumin = mm1 + jumins;
	
	// 주민번호 유효성 검사
    if (jumin == "") {
        alert("주민번호를 입력하세요");
        document.frm.mm1.focus();
        return false;
    } else if (!number.test(jumin) || !isValidJumin(jumin)) {
        alert("유효한 주민번호가 아닙니다");
        document.frm.mm1.focus();
        return false;
    } else {
        // 유효한 주민번호인 경우, 마스킹 처리
        if (mm2.length === 7) {
            let maskJumin = mm2.substring(0, 1).replace(/[0-9a-zA-Z]/g, "*") + mm2.substring(1, 7);
            document.frm.mm2.value = maskJumin;
        }
    }
	


}
```
</details>

<br>
<br>

## 과제 체크박스 조건
1. 전체 체크박스 클릭 시 9개의 항목 체크 <br>
- 체크된 9개의 항목중 1개라도 선택 해제 시 전체 체크 해제
- 전체 체크 다시 체크 시 해재된 항목 체크
2. 항목 체크 한 순서대로 아래에  항목 이름 표시 <br>
예) 부산 서울 경기 울산 <br>
- 체크된 항목 해제 시 아래에 내용 삭제 <br>
예) 부산 서울 경기 울산 || 부산 항목 체크 해제 시 -> 서울 경기 울산 <br>
3. 버튼 클릭 시 3가지 조건 달성
  0개 혹은 4개 이하 체크 된 경우
  전체 항목 체크 된 경우
  그 외 false

## 과제 코딩

check.jsp
<br>

<details>
    <summary>코드 보기</summary>
	
```jsp

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script defer type="text/javascript" src=/js/check.js></script>
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<title>체크박스 과제</title>
</head>
<body>


<div class="box">
	<input type="checkbox" name="all" id="all">전체</input>
	<input type="button" value="버튼" id="btn" name="btn">
	<br>
	<input type="checkbox" name="se" class="aa" value="서울">서울</input>
	<input type="checkbox" name="in" class="aa" value="인천">인천</input>
	<input type="checkbox" name="gy" class="aa" value="경기">경기</input>
	<input type="checkbox" name="ga" class="aa" value="강원">강원</input>
	<input type="checkbox" name="bu" class="aa" value="부산">부산</input>
	<input type="checkbox" name="da" class="aa" value="대전">대전</input>
	<input type="checkbox" name="je" class="aa" value="전남">전남</input>
	<input type="checkbox" name="je" class="aa" value="제주">제주</input>
	<input type="checkbox" name="py" class="aa" value="평양">평양</input>

</div>
<div class="text"></div>

</body>
</html>


```
</details>

<br>
<br>

check.js
<br>

<details>
    <summary>코드 보기</summary>
	
```javascript

$(function(){
	// 전체 체크박스가 클릭
	$('#all').click(function (){
		checkedAll();
	});
	
	// 버튼 클릭 했을 때
	$('#btn').click(function(){
		checkButton();
	});
	// 항목 체크 여부
	$('.aa').click(function(){
		checkedFun();
		
		let checkValue = $(this).val();
	    
	    if($(this).is(":checked")){
	    	$('.text').append('<span>'+ checkValue +'</span>');
	        }else{
	        	// 해제 시
	        	 $('.text').find('span').each(function() {
	                 if ($(this).text() === checkValue) {
	                     $(this).remove();
	                     return false;
	                 }
	             });
	        }
	});
	
});

function checkedAll(){
	let checked = $("input[name=all]").is(':checked');
	let checkValue = $("input[class=aa]").val();
	let checks = $('input:checkbox[class=aa]:not(:checked)');
	
	if(checked){
		// 클릭이 되었다면
		$(".aa").prop("checked", true);
		
			
		$.each(checks, function(index,item){
			$('.text').append('<span>'+ $(item).val() +'</span>');
		});
		
	}else{
		$(".aa").prop("checked", false);
        $('span').remove();
	}
}

function checkButton(){
	// 1개도 선택 안됬을 때
	let checked = $("input[name=all]").is(':checked');
	
	// 체크박스 체크한 개수 구하기
	let checks = $('input:checkbox[class=aa]:checked').length;
	
	if(checks == 0){
		alert("최소 1개 이상 선택 하세요");
	}else if(checked){
		alert("전체를 클릭 하셨습니다!");
	}else if(checks <= 4){
		alert("4개 이하를 선택 하셨습니다");
	}else{
		alert("5개 이상 혹은 그 외 선택");
	}
}


function checkedFun(){
	// 전체 체크
    let checkAll = $("input[name=all]");
    // 체크 항목
    let checkaa = $("input[class=aa]");
    // 항목중에 체크된
    let checkedaa = $("input[class=aa]:checked");
    // 항목 값
   
    if(checkaa.length != checkedaa.length){
    	// 체크안한 항목이 있다면 전체 체크 해제
    	$("#all").prop('checked', false);
    }else{
    	// 모두 체크 시 전체 항목 체크
    	$("#all").prop('checked', true);
    }
 
}
```
</details>


## 느낀점
오래간만에(?) JSP, javascript 사용해 보았는데 뭔가 생소한? 느낌이었고 <br>
까먹은 태그나 사용법은 다시 구글링 치면서 익혔다 <br>
간단한 미니프로젝트를 다양한 주제로 활용해 만들어야 겠다
