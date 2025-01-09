# Урок 1. Коллекции и итераторы. Модули
Формат сдачи: ссылка на репозиторий.


## Задание 1
    • Используя Symbol.iterator, создайте объект "Музыкальная коллекция", который можно итерировать. Каждая итерация должна возвращать следующий альбом из коллекции.

    • Создайте объект musicCollection, который содержит массив альбомов и имеет свойство-символ Symbol.iterator. Каждый альбом имеет следующую структуру:
`
{
title: "Название альбома",
artist: "Исполнитель",
year: "Год выпуска"
}
`

    • Реализуйте кастомный итератор для объекта musicCollection. Итератор должен перебирать альбомы по порядку.

    • Используйте цикл for...of для перебора альбомов в музыкальной коллекции и вывода их на консоль в формате: Название альбома - Исполнитель (Год выпуска)

### Решение

```
console.log('TASK 1');

const musicCollection = {
    albums: []
};

const album1 = {
    title: 'Fireball',
    artist: 'Deep Purple',
    year: 1971
}
const album2 = {
    title: 'Deep Purple In Rock',
    artist: 'Deep Purple',
    year: 1970
}
const album3 = {
    title: 'Lovedrive',
    artist: 'Scorpions',
    year: 1979
}
const album4 = {
    title: 'The visitors',
    artist: 'ABBA',
    year: 1981
}

musicCollection.albums.push(album1);
musicCollection.albums.push(album2);
musicCollection.albums.push(album3);
musicCollection.albums.push(album4);

musicCollection[Symbol.iterator] = function () {
    const albums = this.albums;
    return {
        currIndex: 0,
        next() {
            return (this.currIndex < albums.length) ?
                {done: false, value: albums[this.currIndex++]} :
                {done: true};
        }
    }
};

for (const album of musicCollection)  {
    console.log(`Название альбома: ${album.title} - Исполнитель: ${album.artist} (год выпуска): ${album.year}`);
}

```

## Задание 2

Вы управляете рестораном, в котором работают разные повара, специализирующиеся на определенных блюдах. Клиенты приходят и делают заказы на разные блюда.

Необходимо создать систему управления этими заказами, которая позволит:

    • Отслеживать, какой повар готовит какое блюдо.

    • Записывать, какие блюда заказал каждый клиент.

Используйте коллекции Map для хранения блюд и их поваров, а также для хранения заказов каждого клиента. В качестве ключей для клиентов используйте объекты.

Повара и их специализации:

Виктор - специализация: Пицца. \
Ольга - специализация: Суши. \
Дмитрий - специализация: Десерты.

Блюда и их повара:

Пицца "Маргарита" - повар: Виктор. \
Пицца "Пепперони" - повар: Виктор. \
Суши "Филадельфия" - повар: Ольга. \
Суши "Калифорния" - повар: Ольга. \
Тирамису - повар: Дмитрий. \
Чизкейк - повар: Дмитрий.

Заказы:

Клиент Алексей заказал: Пиццу "Пепперони" и Тирамису. \
Клиент Мария заказала: Суши "Калифорния" и Пиццу "Маргарита". \
Клиент Ирина заказала: Чизкейк.

### Решение

```
console.log('TASK 2');

const dishesCock = new Map();
dishesCock.set('Пицца Маргарита', 'Виктор');
dishesCock.set('Пицца Пепперони', 'Виктор');
dishesCock.set('Суши Филадельфия', 'Ольга');
dishesCock.set('Суши Калифорния', 'Ольга');
dishesCock.set('Тирамису', 'Дмитрий');
dishesCock.set('Чизкейк', 'Дмитрий');

const client1 = {
    name: 'Алексей'
};
const client2 = {
    name: 'Мария'
};
const client3 = {
    name: 'Ирина'
};

const client1Orders = new Set(['Пепперони', 'Тирамису']);
const client2Orders = new Set(['Суши Калифорния', 'Пицца Маргарита']);
const client3Orders = new Set(['Чизкейк']);

const clientsOrders = new Map();
clientsOrders.set(client1, client1Orders);
clientsOrders.set(client2, client2Orders);
clientsOrders.set(client3, client3Orders);

let dish = 'Пицца Маргарита';
console.log(`${dish} готовит ${dishesCock.get(dish)}`);
dish = 'Суши Калифорния';
console.log(`${dish} готовит ${dishesCock.get(dish)}`);

console.log(`Клиент ${client1.name} заказал ${[... clientsOrders.get(client1)]}`);

console.log(`Клиент ${client2.name} заказал ${[... clientsOrders.get(client2)]}`);

```
