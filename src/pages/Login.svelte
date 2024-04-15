<form id="login-form" action="/signup" method="POST">
  <div>로그인 하기</div>
  <div>
    <label for="id">아이디</label>
    <input id="id" name="id" type="text" required />
  </div>
  <div>
    <label for="password">패스워드</label>
    <input id="password" name="password" type="password" required />
  </div>
  <div>
    <button type="submit">로그인</button>
  </div>
  <div id="info"></div>
</form>