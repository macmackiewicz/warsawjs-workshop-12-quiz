# warsawjs-workshop-12-quiz

> Aplikacja stworzona we frameworku Vue na potrzeby WarsawJS Workshop #12

## Etapy

### Etap 1: setup
* zainstalowanie vue-cli: `$ npm install -g vue-cli`

* utworzenie nowego projektu: `$ vue init webpack warsawjs-workshop-12-quiz` (przy pytaniu o vue-router oraz testy wybieramy 'n')

* uruchomienie aplikacji: `$ cd warsawjs-workshop-12-quiz`, `$ npm install`, `$ npm run dev` (rezultat można zobaczyć w przeglądarce pod adresem localhost:8080)

* dodanie Vuetify: `$ npm install vuetify --save`

### Etap 2: struktura
* aktywowanie komponentów Vuetify w projekcie w pliku src/main.js:
```javascript
import Vuetify from 'vuetify'
import 'vuetify/dist/vuetify.min.css'

Vue.use(Vuetify)
```
* usunięcie domyślnego kodu vue-cli z pliku src/App.vue pomiędzy elementami `<template></template>` oraz `<style></style>`, a także wewnątrz `export default {...}`
* dodanie w katalogu src ppliku quiz.js, w którym znajdzie się lista obiektów zawierających pytania, listę odpowiedzi, oraz indeks poprawnej odpowiedzi
* umieszczenie wewnątrz elementu `template` w pliku App.vue podstawowej struktury layoutu:
```html
  <v-app dark>
    <v-content>
      <v-container>
        <v-layout>
          <v-flex>
            <v-card>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
```
### Etap 3: prezentowanie pytań

* zaimportowanie listy z pliku quiz.js
* dodanie w właściwości `data` zmiennej zawierającej informację indeksie aktualnego pytania w quizie
* dodanie w właściwości `computed` metody, która zwróci aktualne pytanie z quizu na podstawie indeksu zdefiniowanego w `data`
* wyświetlenie w elemencie `v-card-title` treści aktualnego pytania

### Etap 4: prezentowanie odpowiedzi
* dodanie w elemencie `v-card-text` listy `v-list`, a w niej iterowanie po odpowiedziach w aktualnym pytaniu za pomocą dyrektywy `v-for` w elemencie `v-card-tile`
* dodanie w właściwości data zmiennej zawierającej indeks wybranego przez użytkownika pytania (domyślnie `null`)
* dodanie do elementu odpowiedzi metody zachowującej indeks odpowiedzi, w którą kliknie użytkownik za pomocą dyrektywy `@click`
* stworzenie w właściwości `methods` metody, która zwróci informację, o tym jaką klasę powinna otrzymać odpowiedź w liście po wybraniu odpowiedzi przez użytkownika:
  - `success`, jeżeli indeks danej odpowiedzi jest taki sam, jak indeks poprawnej odpowiedzi **oraz** indeks danej odpowiedzi jest taki sam, jak indeks, który wybrał użytkownik
  - `error`, jeżeli indeks danej odpowiedzi jest taki sam, jak wybór użytkownika, ale nie jest to poprawna odpowiedź
  - `secondary` w każdym innym przypadku

### Etap 5: przejście do kolejnych pytań
* dodanie elementu `v-card-actions`, w którym znajdą się dwa przyciski `v-btn`
* pierwszy powinien być widoczny, jeżeli użytkownik wybrał poprawną odpowiedź (dzięki dyrektywie `v-if`) i wywoływać metodę inkrementującą indeks aktualnego pytania
* następny powinien być widoczny, jeżeli użytkownik wybrał złą odpowiedź i wywoływać metodę resetującą indeks aktualnego pytania na 0

### Etap 6: wyświetlenie informacji o wygranej
* dodanie w `computed` metody, która spradzi, czy użytkownik odpowiedział na wszystkie pytania, jeżeli tak, powinniśmy go poinformować o tym, że wygrał

### Etap 7: github
* założenie na githubie projektu warsawjs-workshop-12-quiz i umieszczenie w nim aplikacji stworzonej na warsztatach
