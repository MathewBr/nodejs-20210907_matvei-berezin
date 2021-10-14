# Онлайн-магазин (товары и категории)

В этом задании вам предстоит реализовать получение списка категорий, списка товаров по конкретной
подкатегории, а также товара по его идентификатору. Это необходимая часть для работы нашего будущего
интернет-магазина.

В общем случае процесс обработки запроса разделяется на следующие этапы:
1. Обработка запроса (получение параметров, определение условий)
2. Получение необходимых данных из базы данных (в зависимости от условий, определенных на предыдущем
этапе).
3. Преобразование данных из базы данных в тот вид, который необходимо вернуть.


## Получение списка категорий

| Метод | Ссылка          | Описание                   | Параметры |
|-------|-----------------|----------------------------|-----------|
| GET   | /api/categories | Получение списка категорий | -         |

Пример запроса: `http://localhost:3000/api/categories`

Пример ответа сервера:
```js
{
  categories: [
    {
    id: '5d208e631866a7366d831ffc',
    title: 'Category1',
    subcategories: [{
      id: '5d208e631866a7366d831ffd',
      title: 'Subcategory1'
    }]
  }
  ]
}
```
Обратите внимание, тот формат что мы возвращаем отличается от того формата, который находится в базе данных. Это
преобразование нужно выполнить на сервере перед тем, как возвращать ответ пользователю.

## Получение товаров

### По подкатегории

Важный момент: запрос делается именно по идентификатору подкатегории, а не просто категории.

| Метод | Ссылка          | Описание                   | Параметры   |
|-------|-----------------|----------------------------|-------------|
| GET   | /api/products   | Получение списка товаров   | subcategory |

Пример запроса: `http://localhost:3000/api/products?subcategory=5d20cf5bba02bff789f8e29e`

Пример ответа сервера:
```js
{
  products: [
    {
      id: '5d20cf5bba02bff789f8e29f',
      title: 'Product1',
      images: ['image1', 'image2'],
      category: '5d20cf5bba02bff789f8e29d',
      subcategory: '5d20cf5bba02bff789f8e29e',
      price: 10,
      description: 'Description1'
    }
  ]
}
```

### По идентификатору

Этот метод должен возвращать товар из базы по его идентификатору. Идентификатор должен быть валидным
`ObjectId`, если переданный идентификатор невалидный - сервер должен вернуть ошибку со статусом
`400`. Если товара с заданным идентификатором нет - сервер должен вернуть ошибку со статусом `404`.

| Метод | Ссылка              | Описание                             | Параметры   |
|-------|---------------------|--------------------------------------|-------------|
| GET   | /api/products/:id   | Получение товара по идентификатору   |             |

Пример запроса: `http://localhost:3000/api/products/5d20d32d3a0676032a9a3174`

Пример ответа сервера:
```js
{
  product: {
    id: '5d20d32d3a0676032a9a3174',
    title: 'Product1',
    images: [ 'image1' ],
    category: '5d20d32d3a0676032a9a3172',
    subcategory: '5d20d32d3a0676032a9a3173',
    price: 10,
    description: 'Description1'
  }
}
```
