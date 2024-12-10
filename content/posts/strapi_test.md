---
title: "Пример страницы с API-запросом и Authorization"
date: 2024-12-09
---

# Данные из API

<p id="api-data">Загрузка данных...</p>

<script>
  // Функция для получения данных из API с заголовком Authorization
  async function fetchData() {
    try {
      const response = await fetch('http://138.124.52.135:1337/api/articles', {
        method: 'GET',
        headers: {
          'Authorization': 'Bearer 07e99e8881150195cbb253bcf58655c5fdecd34ad87e8da085e53f5b765bc164cd1e38cbd584336f3e332a1853a4fbfef1a1af86fc52233df87d29b0e51019671b9a24a962f57816d5e4909c2a4e6f8c4b37c6a6a9aa5ac8fc92a4f7eee32c38cecda0906cc985c3adf0eaa422094d9f55f1b79ca48604783133898745a9631a',  // Замените на ваш токен
          'Content-Type': 'application/json'
        }
      });

      // Проверка успешности запроса
      if (!response.ok) {
        throw new Error('Ошибка при запросе данных');
      }

      const data = await response.json();
      
      // Обрабатываем массив статей
      const articles = data.data;  // Извлекаем массив статей из объекта 'data'
      
      // Создаем строку для отображения всех заголовков
      let articlesList = articles.map(article => `<li>${article.attributes.title}</li>`).join('');

      // Обновляем содержимое элемента на странице
      document.getElementById('api-data').innerHTML = `<ul>${articlesList}</ul>`;
    } catch (error) {
      console.error('Ошибка при запросе:', error);
      document.getElementById('api-data').innerText = 'Ошибка при загрузке данных.';
    }
  }

  // Вызов функции при загрузке страницы
  fetchData();
</script>