<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>서버 실행 및 외부 네트워크 접속 가이드</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
            background-color: #f9f9f9;
            color: #333;
        }
        h1, h2 {
            color: #2c3e50;
        }
        pre {
            background: #ecf0f1;
            padding: 10px;
            border: 1px solid #bdc3c7;
            border-radius: 5px;
            overflow-x: auto;
        }
        ul, ol {
            margin: 15px 0;
            padding-left: 20px;
        }
        li {
            margin-bottom: 10px;
        }
        a {
            color: #2980b9;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h1>서버 실행 및 외부 네트워크 접속 가이드</h1>
    <p>이 가이드는 로컬 컴퓨터에서 서버를 실행하고, 외부 네트워크(다른 네트워크)에서 해당 서버에 접속하는 방법을 단계별로 설명합니다.</p>

    <h2>1. Spring Boot 서버 실행</h2>
    <ol>
        <li>Spring Boot 프로젝트 디렉토리에서 다음 명령어를 실행합니다:
            <pre><code>./gradlew bootRun</code></pre>
        </li>
        <li>브라우저에서 다음 주소로 서버가 실행 중인지 확인합니다:
            <pre><code>http://localhost:8080</code></pre>
        </li>
    </ol>

    <h2>2. 서버의 내부 IP 주소 확인</h2>
    <ol>
        <li>명령 프롬프트(cmd)를 열고 다음 명령어를 실행합니다:
            <pre><code>ipconfig</code></pre>
        </li>
        <li>출력된 결과에서 <b>IPv4 주소</b>를 확인합니다. 예: <code>192.168.219.103</code></li>
    </ol>

    <h2>3. 공용 IP 주소 확인</h2>
    <ol>
        <li>브라우저에서 <a href="https://ip.pe.kr" target="_blank">ip.pe.kr</a>에 접속합니다.</li>
        <li>공용 IP 주소를 확인합니다. 예: <code>49.165.191.3</code></li>
    </ol>

    <h2>4. 포트 포워딩 설정</h2>
    <ol>
        <li>브라우저에서 라우터 관리자 페이지(기본 게이트웨이 주소, 예: <code>192.168.219.1</code>)로 접속합니다.</li>
        <li>로그인한 후 <b>포트 포워딩</b> 또는 <b>NAT 설정</b> 메뉴로 이동합니다.</li>
        <li>다음 정보를 입력하여 포트 포워딩을 설정합니다:
            <ul>
                <li><b>서비스 포트:</b> 8080 - 8080</li>
                <li><b>프로토콜:</b> TCP</li>
                <li><b>내부 IP 주소:</b> 192.168.219.103</li>
                <li><b>내부 포트:</b> 8080</li>
            </ul>
        </li>
        <li>설정을 저장하고 라우터를 재부팅합니다.</li>
    </ol>

    <h2>5. Windows 방화벽에서 8080 포트 열기</h2>
    <ol>
        <li>Windows 검색창에서 "방화벽"을 입력하고 <b>고급 보안이 포함된 Windows Defender 방화벽</b>을 실행합니다.</li>
        <li>왼쪽에서 <b>인바운드 규칙</b>을 선택하고, 오른쪽에서 <b>새 규칙</b>을 클릭합니다.</li>
        <li>규칙 설정:
            <ul>
                <li><b>규칙 유형:</b> 포트</li>
                <li><b>프로토콜:</b> TCP</li>
                <li><b>포트 번호:</b> 8080</li>
                <li><b>작업:</b> 연결 허용</li>
                <li><b>프로필:</b> 도메인, 개인, 공용</li>
                <li><b>이름:</b> Spring Boot 8080</li>
            </ul>
        </li>
    </ol>

    <h2>6. 외부 네트워크에서 접속</h2>
    <ol>
        <li>외부 네트워크(예: 모바일 데이터)에 연결된 장치에서 브라우저를 열고 다음 주소로 접속합니다:
            <pre><code>http://49.165.191.3:8080/api/users/view</code></pre>
        </li>
    </ol>

    <h2>7. 네트워크 논리</h2>
    <ul>
        <li><b>클라이언트 → 라우터:</b> 클라이언트는 공용 IP와 포트를 사용하여 라우터에 요청을 보냅니다.</li>
        <li><b>라우터 → 서버:</b> 라우터는 포트 포워딩 설정을 통해 요청을 내부 서버로 전달합니다.</li>
        <li><b>서버 → 클라이언트:</b> 서버는 요청을 처리한 후 클라이언트로 응답을 반환합니다.</li>
    </ul>

    <h2>8. 추가 참고사항</h2>
    <ul>
        <li>공용 IP가 변경될 수 있으므로 고정 IP 또는 DDNS 서비스를 고려하세요.</li>
        <li>사용하지 않을 때는 포트 포워딩 설정을 비활성화하여 보안을 강화하세요.</li>
    </ul>
</body>
</html>
