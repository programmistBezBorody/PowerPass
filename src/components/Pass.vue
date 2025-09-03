<template>
    <div class="password-power">
        <label for="password-input">
            Пароль
        </label>
        <input type="password" 
                id="password-input" 
                class="password-input"
        >
        <div class="progress-bar-container">
            <div class="progress-bar">

            </div>
        </div>
        <div class="power-text">

        </div>
        <div class="requirement">
            <p>Требования к паролю: </p>
            <ul>
                <li>Минимум 8 символов</li>
                <li>Содержит заглавные буквы</li>
                <li>Содержит строчные буквы</li>
                <li>Содержит цифры</li>
                <li>Содержит специальные символы</li>
            </ul>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>
    .password-power {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.password-input {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border: 2px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  box-sizing: border-box;
}

.password-input:focus {
  outline: none;
  border-color: #4CAF50;
}

.progress-bar-container {
  width: 100%;
  height: 10px;
  background-color: #f0f0f0;
  border-radius: 5px;
  overflow: hidden;
  margin: 10px 0;
}

.progress-bar {
  height: 100%;
  transition: width 0.3s ease, background-color 0.3s ease;
}

.progress-bar.weak {
  background-color: #ff4757; /* Красный для слабого пароля */
}

.progress-bar.medium {
  background-color: #ffa502; /* Желтый для среднего пароля */
}

.progress-bar.strong {
  background-color: #2ed573; /* Зеленый для надежного пароля */
}

.strength-text {
  text-align: center;
  font-weight: bold;
  margin: 5px 0;
}

.strength-text.weak {
  color: #ff4757;
}

.strength-text.medium {
  color: #ffa502;
}

.strength-text.strong {
  color: #2ed573;
}

.requirement {
  margin-top: 15px;
  padding: 10px;
  background-color: #f9f9f9;
  border-radius: 4px;
}

.requirement ul {
  list-style: none;
  padding: 0;
  margin: 10px 0 0 0;
}

.requirement li {
  padding: 5px 0;
  color: #ff4757;
}

.requirement li.met {
  color: #2ed573;
  text-decoration: line-through;
}

.requirement p {
  margin: 0;
  font-weight: bold;
}
</style>