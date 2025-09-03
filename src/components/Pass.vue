<template>
    <div class="password-power">
        <label for="password-input">
            Пароль
        </label>
        <input type="password" 
                id="password-input" 
                class="password-input"
                v-model="password"
                placeholder="Введите пароль"
        >
        <div class="progress-bar-container">
            <div class="progress-bar"
                :style="progressBarStyle"
                :class="strengthClass"
            >

            </div>
        </div>
        <div class="power-text"
            :class="strengthClass"
        >
            {{ powerText }}
        </div>
        <div class="requirement"
            v-if="password.length > 0"
        >
            <p>Требования к паролю: </p>
            <ul>
                <li :class="{'met': hasMinLength}">Минимум 8 символов</li>
                <li :class="{'met': hasUppercase}">Содержит заглавные буквы</li>
                <li :class="{'met': hasLowercase}">Содержит строчные буквы</li>
                <li :class="{'met': hasDigits}">Содержит цифры</li>
                <li :class="{'met': hasSpecialChars}">Содержит специальные символы</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
    import { ref, computed, watch } from 'vue';

    const password = ref('');

    // Критерии проверки пароля
    const hasMinLength = computed(() => password.value.length >= 8);
    const hasUppercase = computed(() => /[A-Z]/.test(password.value));
    const hasLowercase = computed(() => /[a-z]/.test(password.value));
    const hasSpecialChars = computed(() => /[!@#$%^&*(),.?":{}|<>]/.test(password.value));
    const hasDigits = computed(() => /\d/.test(password.value));

    // Подсчет выполнения критериев
    const criterialCount = computed(() => {
        return [
            hasMinLength.value,
            hasUppercase.value,
            hasLowercase.value,
            hasSpecialChars.value,
            hasDigits.value
        ].filter(Boolean).length
    });

    // Процент выполнения
    const powerPercent = computed(() => {
        return (criterialCount / 5) * 100;
    });
    
    // Определение уровня надежности
    const strengthLevel = computed(() => {
        if (criterialCount.value === 0) return 0
        if (criterialCount.value <= 2) return 1 // Слабый
        if (criterialCount.value <= 4) return 2 // Средний
        return 3 // Сильный
    })

    // Стиль прогресс-бара
    const progressBarStyle = computed(() => ({
        width: `${powerPercent.value}%`
    }))

// Класс для стилизации по уровню надежности
    const strengthClass = computed(() => {
    switch (strengthLevel.value) {
        case 1: return 'weak'
        case 2: return 'medium'
        case 3: return 'strong'
        default: return ''
    }
    })

// Текст описания надежности
const powerText = computed(() => {
  switch (strengthLevel.value) {
    case 1: return 'Слабый пароль'
    case 2: return 'Средний пароль'
    case 3: return 'Надежный пароль'
    default: return 'Введите пароль'
  }
})


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