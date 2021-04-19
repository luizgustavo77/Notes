# **Coockie**
> Variavel que normalmente referencia uma sessão entre o usuario e o servidor com no máximo 4 KB separados por ponto e vírgula e salva no lado do usuario. **Como funciona?** Quando um navegador solicita uma página da Web de um servidor, os cookies pertencentes à página são adicionados à solicitação. Dessa forma, o servidor obtém os dados necessários para "lembrar" as informações sobre os usuários.
- **Create**
``` javascript
function setCookie(cname, cvalue, exdays) {
  var d = new Date();
  d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
  var expires = "expires="+d.toUTCString();
  document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
}
```
- **Get**
``` javascript
function getCookie(cname) {
  var name = cname + "=";
  var ca = document.cookie.split(';');
  for(var i = 0; i < ca.length; i++) {
    var c = ca[i];
    while (c.charAt(0) == ' ') {
      c = c.substring(1);
    }
    if (c.indexOf(name) == 0) {
      return c.substring(name.length, c.length);
    }
  }
  return "";
}
``` 
- **Check**
``` javascript
function checkCookie() {
  var user = getCookie("username");
  if (user != "") {
    alert("Welcome again " + user);
  } else {
    user = prompt("Please enter your name:", "");
    if (user != "" && user != null) {
      setCookie("username", user, 365);
    }
  }
}
```
- **Delete**
> Basta definir o parâmetro expires para uma data passada
``` javascript
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
```
