# JavaScript

<figure><img src=".gitbook/assets/javascript.jpg" alt=""><figcaption></figcaption></figure>

En: What is Javascprit? What does it do? What are the commands? Here are the short and concise answers to your questions.

TR: Javascprit nedir? Ne işe yarar? Komutlar nelerdir? İşte sorularınızın kısa ve öz cevapları.

### What is JavaScript?

JavaScript is a programming language that makes web pages interactive and dynamic. Along with HTML and CSS, it is one of the core technologies of the internet.

### What Does JavaScript Do?

* Animated elements and animations can be created.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
      body {
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #222;
      }

      .circle {
        width: 100px;
        height: 100px;
        background-color: #3498db;
        border-radius: 50%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        animation: move 2s ease-in-out infinite alternate;
      }

      @keyframes move {
        0% {
          transform: translate(-50%, -50%) rotate(0deg);
          background-color: #3498db;
        }
        50% {
          transform: translate(-50%, -50%) rotate(180deg);
          background-color: #e74c3c;
        }
        100% {
          transform: translate(-50%, -50%) rotate(360deg);
          background-color: #3498db;
        }
      }
    </style>
  </head>
  <body>
    <div class="circle"></div>
  </body>
</html>

```

* Can update data dynamically.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <h1 id="data"></h1>

    <script>
      
      function updateData() {
        var randomNumber = Math.floor(Math.random() * 100);

        document.getElementById("data").innerText =
          "Random Number: " + randomNumber;
      }

      updateData();
      setInterval(updateData, 2000);
   
     </script>
  </body>
</html>

```

* Can validate forms.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <form id="myForm" onsubmit="return validateForm()">
      <label for="username">Kullanıcı Adı:</label><br />
      <input type="text" id="username" name="username" /><br />
      <label for="password">Şifre:</label><br />
      <input type="password" id="password" name="password" /><br /><br />
      <button type="submit">Gönder</button>
    </form>

    <div id="error"></div>

    <script>
      function validateForm() {
        var username = document.getElementById("username").value;
        var password = document.getElementById("password").value;
        var errorElement = document.getElementById("error");
        errorElement.innerHTML = "";

        if (username.trim() === "") {
          errorElement.innerText = "Username cannot be blank";
          return false;
        }

        if (password.trim() === "" || password.length < 6) {
          errorElement.innerText =
            "Password cannot be blank and must be at least 6 characters";
          return false;
        }

        return true;
      }
    </script>
  </body>
</html>

```

* Single Page Apps (SPAs) can be developed.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
      </ul>
    </nav>

    <div id="app"></div>

    <script>
      const views = {
        home: `<h1>Welcome to the Home Page!</h1>`,
        about: `<h1>About Us</h1>
            <p>This is a simple Single Page Application example.</p>`,
      };

      function render(view) {
        document.getElementById("app").innerHTML = views[view];
      }

      function navigate() {
        const route = window.location.hash.substring(1);
        render(route || "home");
      }

      window.addEventListener("hashchange", navigate);

      navigate();
    </script>
  </body>
</html>
```

* Web games and interactive applications can be developed.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <h1>Guess the Number Game</h1>

    <label for="guessField">Enter a guess: </label>
    <input type="text" id="guessField" class="guessField" />
    <input type="submit" value="Submit guess" class="guessSubmit" />

    <p class="guesses"></p>
    <p class="lastResult"></p>
    <p class="lowOrHi"></p>

    <script>
      let randomNumber = Math.floor(Math.random() * 100) + 1;
      const guesses = document.querySelector(".guesses");
      const lastResult = document.querySelector(".lastResult");
      const lowOrHi = document.querySelector(".lowOrHi");

      const guessSubmit = document.querySelector(".guessSubmit");
      const guessField = document.querySelector(".guessField");

      let guessCount = 1;
      let resetButton;

      function checkGuess() {
        let userGuess = Number(guessField.value);
        if (guessCount === 1) {
          guesses.textContent = "Previous guesses: ";
        }
        guesses.textContent += userGuess + " ";

        if (userGuess === randomNumber) {
          lastResult.textContent = "Congratulations! You got it right!";
          lastResult.style.backgroundColor = "green";
          lowOrHi.textContent = "";
          setGameOver();
        } else if (guessCount === 10) {
          lastResult.textContent = "!!!GAME OVER!!!";
          setGameOver();
        } else {
          lastResult.textContent = "Wrong!";
          lastResult.style.backgroundColor = "red";
          if (userGuess < randomNumber) {
            lowOrHi.textContent = "Last guess was too low!";
          } else if (userGuess > randomNumber) {
            lowOrHi.textContent = "Last guess was too high!";
          }
        }

        guessCount++;
        guessField.value = "";
        guessField.focus();
      }

      guessSubmit.addEventListener("click", checkGuess);

      function setGameOver() {
        guessField.disabled = true;
        guessSubmit.disabled = true;
        resetButton = document.createElement("button");
        resetButton.textContent = "Start new game";
        document.body.appendChild(resetButton);
        resetButton.addEventListener("click", resetGame);
      }

      function resetGame() {
        guessCount = 1;
        const resetParas = document.querySelectorAll(".resultParas p");
        for (let i = 0; i < resetParas.length; i++) {
          resetParas[i].textContent = "";
        }

        resetButton.parentNode.removeChild(resetButton);
        guessField.disabled = false;
        guessSubmit.disabled = false;
        guessField.value = "";
        guessField.focus();

        lastResult.style.backgroundColor = "white";

        randomNumber = Math.floor(Math.random() * 100) + 1;
      }
    </script>
  </body>
</html>
```

* Communicate with APIs.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <h1>Posts</h1>

    <ul id="posts"></ul>

    <script>
      const url = "https://jsonplaceholder.typicode.com/posts";

      fetch(url)
        .then((response) => response.json())
        .then((data) => {
          const postsElement = document.getElementById("posts");

          data.forEach((post) => {
            const li = document.createElement("li");
            li.textContent = post.title;
            postsElement.appendChild(li);
          });
        })
        .catch((error) => console.error("Error fetching data:", error));
    </script>
  </body>
</html>
```

The above examples are simple ones. But now most of the websites or most of the applications used all over the world are dynamic websites built with JavaScript and JavaScript Fremeworks.

{% hint style="info" %}
Framework is a structure used to accelerate, standardize and make software development processes more efficient.

Sample Javascript Frameworks:

1. React
2. Angular
3. Vue.js
4. Ember.js
5. Backbone.js
6. Svelte
7. Meteor
8. Polymer
9. Aurelia
10. Express.js
{% endhint %}

For example, social media platforms (Facebook, Twitter, Instagram), e-commerce websites (Amazon, eBay, Alibaba), news websites (CNN, BBC, New York Times), search engines (Google, Bing), video sharing platforms (YouTube, Netflix), and many other websites actively use JavaScript.



### JavaScript Nedir?

JavaScript, web sayfalarını etkileşimli ve dinamik hale getiren bir programlama dilidir. HTML ve CSS ile birlikte internetin temel teknolojilerinden biridir.

### JavaScript Ne İşe Yarar?

* Animasyonlu öğeler ve animasyonlar oluşturulabilir.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
      body {
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #222;
      }

      .circle {
        width: 100px;
        height: 100px;
        background-color: #3498db;
        border-radius: 50%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        animation: move 2s ease-in-out infinite alternate;
      }

      @keyframes move {
        0% {
          transform: translate(-50%, -50%) rotate(0deg);
          background-color: #3498db;
        }
        50% {
          transform: translate(-50%, -50%) rotate(180deg);
          background-color: #e74c3c;
        }
        100% {
          transform: translate(-50%, -50%) rotate(360deg);
          background-color: #3498db;
        }
      }
    </style>
  </head>
  <body>
    <div class="circle"></div>
  </body>
</html>

```

* Verileri dinamik olarak güncelleyebilir.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <h1 id="data"></h1>

    <script>
      
      function updateData() {
        var randomNumber = Math.floor(Math.random() * 100);

        document.getElementById("data").innerText =
          "Random Number: " + randomNumber;
      }

      updateData();
      setInterval(updateData, 2000);
   
     </script>
  </body>
</html>

```

* Formları doğrulayabilir.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <form id="myForm" onsubmit="return validateForm()">
      <label for="username">Kullanıcı Adı:</label><br />
      <input type="text" id="username" name="username" /><br />
      <label for="password">Şifre:</label><br />
      <input type="password" id="password" name="password" /><br /><br />
      <button type="submit">Gönder</button>
    </form>

    <div id="error"></div>

    <script>
      function validateForm() {
        var username = document.getElementById("username").value;
        var password = document.getElementById("password").value;
        var errorElement = document.getElementById("error");
        errorElement.innerHTML = "";

        if (username.trim() === "") {
          errorElement.innerText = "Username cannot be blank";
          return false;
        }

        if (password.trim() === "" || password.length < 6) {
          errorElement.innerText =
            "Password cannot be blank and must be at least 6 characters";
          return false;
        }

        return true;
      }
    </script>
  </body>
</html>

```

* Tek Sayfa Uygulamaları (SPA'lar) geliştirilebilir.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
      </ul>
    </nav>

    <div id="app"></div>

    <script>
      const views = {
        home: `<h1>Welcome to the Home Page!</h1>`,
        about: `<h1>About Us</h1>
            <p>This is a simple Single Page Application example.</p>`,
      };

      function render(view) {
        document.getElementById("app").innerHTML = views[view];
      }

      function navigate() {
        const route = window.location.hash.substring(1);
        render(route || "home");
      }

      window.addEventListener("hashchange", navigate);

      navigate();
    </script>
  </body>
</html>
```

* Web oyunları ve interaktif uygulamalar geliştirilebilir.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <h1>Guess the Number Game</h1>

    <label for="guessField">Enter a guess: </label>
    <input type="text" id="guessField" class="guessField" />
    <input type="submit" value="Submit guess" class="guessSubmit" />

    <p class="guesses"></p>
    <p class="lastResult"></p>
    <p class="lowOrHi"></p>

    <script>
      let randomNumber = Math.floor(Math.random() * 100) + 1;
      const guesses = document.querySelector(".guesses");
      const lastResult = document.querySelector(".lastResult");
      const lowOrHi = document.querySelector(".lowOrHi");

      const guessSubmit = document.querySelector(".guessSubmit");
      const guessField = document.querySelector(".guessField");

      let guessCount = 1;
      let resetButton;

      function checkGuess() {
        let userGuess = Number(guessField.value);
        if (guessCount === 1) {
          guesses.textContent = "Previous guesses: ";
        }
        guesses.textContent += userGuess + " ";

        if (userGuess === randomNumber) {
          lastResult.textContent = "Congratulations! You got it right!";
          lastResult.style.backgroundColor = "green";
          lowOrHi.textContent = "";
          setGameOver();
        } else if (guessCount === 10) {
          lastResult.textContent = "!!!GAME OVER!!!";
          setGameOver();
        } else {
          lastResult.textContent = "Wrong!";
          lastResult.style.backgroundColor = "red";
          if (userGuess < randomNumber) {
            lowOrHi.textContent = "Last guess was too low!";
          } else if (userGuess > randomNumber) {
            lowOrHi.textContent = "Last guess was too high!";
          }
        }

        guessCount++;
        guessField.value = "";
        guessField.focus();
      }

      guessSubmit.addEventListener("click", checkGuess);

      function setGameOver() {
        guessField.disabled = true;
        guessSubmit.disabled = true;
        resetButton = document.createElement("button");
        resetButton.textContent = "Start new game";
        document.body.appendChild(resetButton);
        resetButton.addEventListener("click", resetGame);
      }

      function resetGame() {
        guessCount = 1;
        const resetParas = document.querySelectorAll(".resultParas p");
        for (let i = 0; i < resetParas.length; i++) {
          resetParas[i].textContent = "";
        }

        resetButton.parentNode.removeChild(resetButton);
        guessField.disabled = false;
        guessSubmit.disabled = false;
        guessField.value = "";
        guessField.focus();

        lastResult.style.backgroundColor = "white";

        randomNumber = Math.floor(Math.random() * 100) + 1;
      }
    </script>
  </body>
</html>
```

* API'ler ile iletişim kurabilir.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  <body>
    <h1>Posts</h1>

    <ul id="posts"></ul>

    <script>
      const url = "https://jsonplaceholder.typicode.com/posts";

      fetch(url)
        .then((response) => response.json())
        .then((data) => {
          const postsElement = document.getElementById("posts");

          data.forEach((post) => {
            const li = document.createElement("li");
            li.textContent = post.title;
            postsElement.appendChild(li);
          });
        })
        .catch((error) => console.error("Error fetching data:", error));
    </script>
  </body>
</html>
```

Yukarıdaki örnekler basit örneklerdir. Ancak artık tüm dünyada kullanılan web sitelerinin veya uygulamaların çoğu JavaScript ve JavaScript Fremeworks ile oluşturulmuş dinamik web siteleridir.

{% hint style="info" %}
Framework, yazılım geliştirme süreçlerini hızlandırmak, standartlaştırmak ve daha verimli hale getirmek için kullanılan bir yapıdır. Örnek Javascript Frameworkleri:&#x20;

1\. React&#x20;

2\. Açısal&#x20;

3\. Vue.js

4\. Ember.js&#x20;

5\. Backbone.js&#x20;

6\. Svelte&#x20;

7\. Meteor&#x20;

8\. Polimer

9\. Aurelia&#x20;

10\. Express.js
{% endhint %}

Örneğin, sosyal medya platformları (Facebook, Twitter, Instagram), e-ticaret siteleri (Amazon, eBay, Alibaba), haber siteleri (CNN, BBC, New York Times), arama motorları (Google, Bing), video paylaşım platformları (YouTube, Netflix) ve diğer birçok web sitesi JavaScript'i aktif olarak kullanmaktadır.
