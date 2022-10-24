

# NgrxNxWorkshop

This project was generated using [Nx](https://nx.dev).

<p style="text-align: center;"><img src="https://raw.githubusercontent.com/nrwl/nx/master/images/nx-logo.png" width="450"></p>

🔎 **Smart, Fast and Extensible Build System**

## Quick Start & Documentation

[Nx Documentation](https://nx.dev/angular)

[10-minute video showing all Nx features](https://nx.dev/getting-started/intro)

[Interactive Tutorial](https://nx.dev/tutorial/01-create-application)

## Adding capabilities to your workspace

Nx supports many plugins which add capabilities for developing different types of applications and different tools.

These capabilities include generating applications, libraries, etc as well as the devtools to test, and build projects as well.

Below are our core plugins:

- [Angular](https://angular.io)
  - `ng add @nrwl/angular`
- [React](https://reactjs.org)
  - `ng add @nrwl/react`
- Web (no framework frontends)
  - `ng add @nrwl/web`
- [Nest](https://nestjs.com)
  - `ng add @nrwl/nest`
- [Express](https://expressjs.com)
  - `ng add @nrwl/express`
- [Node](https://nodejs.org)
  - `ng add @nrwl/node`

There are also many [community plugins](https://nx.dev/community) you could add.

## Generate an application

Run `ng g @nrwl/angular:app my-app` to generate an application.

> You can use any of the plugins above to generate applications as well.

When using Nx, you can create multiple applications and libraries in the same workspace.

## Generate a library

Run `ng g @nrwl/angular:lib my-lib` to generate a library.

> You can also use any of the plugins above to generate libraries as well.

Libraries are shareable across libraries and applications. They can be imported from `@ngrx-nx-workshop/mylib`.

## Development server

Run `ng serve my-app` for a dev server. Navigate to http://localhost:4200/. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng g component my-component --project=my-app` to generate a new component.

## Build

Run `ng build my-app` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test my-app` to execute the unit tests via [Jest](https://jestjs.io).

Run `nx affected:test` to execute the unit tests affected by a change.

## Running end-to-end tests

Run `ng e2e my-app` to execute the end-to-end tests via [Cypress](https://www.cypress.io).

Run `nx affected:e2e` to execute the end-to-end tests affected by a change.

## Understand your workspace

Run `nx dep-graph` to see a diagram of the dependencies of your projects.

## Further help

Visit the [Nx Documentation](https://nx.dev/angular) to learn more.






## ☁ Nx Cloud

### Distributed Computation Caching & Distributed Task Execution

<p style="text-align: center;"><img src="https://raw.githubusercontent.com/nrwl/nx/master/images/nx-cloud-card.png"></p>

Nx Cloud pairs with Nx in order to enable you to build and test code more rapidly, by up to 10 times. Even teams that are new to Nx can connect to Nx Cloud and start saving time instantly.

Teams using Nx gain the advantage of building full-stack applications with their preferred framework alongside Nx’s advanced code generation and project dependency graph, plus a unified experience for both frontend and backend developers.

Visit [Nx Cloud](https://nx.app/) to learn more.

# Notatki do prezentacji
Najlepije przechodzić między tagami i patrzec co sie zmienia np. git checkout m1

## M1
### Push Pull system
Zamiast mieć serwis który tylko ma metody które zwracają observable, można podejść do tego, że jest serwis z BehvaiorSubject, który trzyma stan, a metody zwracają voidy i tylko updatują obiekt. Przykład CartSerice
### shareReplay({ bufferSize: 1, refCount: true })
ShareReplay zawsze dodawać, refCount = true, bo inaczej nawet jak uzywamy async pipe to będzie dalej żyła subsrypcja, chyba, że mamy singletona i chcemy, żeby żył observable nawet gdy nie ma żadnej subsrypcji.
### Cel komponentu
Functions over data => bardzo proste przetworzenia danych tylko w komponencie, logika powinna być wydzielona w inne miejsce

## M2: Action, reducer $ selector
### Action
Action to zwykły obiekt który jest jakby eventem i potem torzymy go przy pomocy factory. Traktować action jako event a nie jako Command, czyli OtworzonoEkran, a nie PobierzProdukty. Trzymać je tam gdzie one sa wywoływane, a nie handlowane.
export const login = createAction(
'[Login Page] Login',
props<{username: string; password: string;}>(),
)
### Reducer
Reducer => Hanlder eventów w zasadzie, powinien byc tylko jeden reducer który zarządza danymi rzeczami?, żeby nie było że jest wiele reducerów z tymi samymi akcjami

### Selector
Select => funkcja do pozyskania danych ze store

### StoreDevtoolModule
Narzędzie do debugowania, przeglądania jakie są stany.

### ts.dev/style/
Style Guide TypeScript

## M3: Efects
### Efects: asychnroncizne zapytania, regaują na akcje i tworzą nowe.
Efekty to klasy (injectable), wiele akcji może rozpocząc dany efekt.
Jka mamy terminalny efekt to dodajemy, {dispatch: false}

## M4: Feature State
### Feature State
Żeby nie trzymać golabl state to możemy mieć feature state Ogólnie to polega na stwrozyć consstant key, który jest taki sam jak w global state, i potem w module, w którym chcemy tym zarządzać uzyjemy .forFeature

### Selector
Używać selectorów bo możemy robić takie chainy, że będą zależały od siebie oraz wydajnościowo to ejst duzo lepsze, bo patrzy na stany, czy sie nie zmieniły stany i nie zrobi rekalkulacji
Gdy uzywamy selectorów przekazujemy 

this.store.select(<naszSelektor>) jest to trochę jak Query w CQRS, wyciaga to ze store, i możemy miec kilka, np. przechowujemy w store listę obiektów i możemy dodać selektor który bazuje na tamtym i potem np. zlicza liczbe obiektów

## M5 Efekty które same się inicjalizuja
Można stworzyć efekty, które same sie inicjalizują np. na podstawie timera

## M6
Czasami chcemy, żeby od razu pokazać zmiane, nawet jak nie wiemy kiedy sie powiedzie, a dopiero potem hanldować błąd

## M7 Router store
Trzymanie w store, informacji o routingu, jaki jest url itd. nie trzeba dzieki temu za każdym razem pisać, tych rzeczy od nowa, już jest zaimplementowany routerReducer i nie musisz tego robić wielokrotnie, trzeba to tylko podpiąc w routerModule

## M8 Combining Selectors
Ogólnie mózg rozjebany, tutaj sie robi cała magia, wykorzystywanie kilku rzeczy trzymanych w store, w tym np. scieżki która jest w url, i możesz uzywać w efektach selektorów.

## M9 View Model
Ogólnie łączenie selektorów w View Model, to akurat robiliśmy wiele razy u nas w smubob

## M10 Entities
Zarządzanie kolekcją objektów w js jest upierdliwe, jest paczka Entities, która pozwala wrapowac kolekcje obiektów, żeby był łatwiejszy dostęp do Kolekcji, którę jest jak w EntityFramework

## M11 call state
Przetrzymywanie infomracji, o zapytaniu http

## M12 Component store
W zasadzie to jest to serwis, który uzywalismy w smubobie, potem wew tego component store, korzytamy z global store. Zawiera całą logikę ekranu, wywołuje global store, albo inne metody z serwisów.
