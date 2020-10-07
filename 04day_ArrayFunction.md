# 자바스크립트 1일 1프로젝트 [4. 배열 함수 연습]

```jsx
// index.html 공통

const inventors = [
        { first: "Albert", last: "Einstein", year: 1879, passed: 1955 },
        { first: "Isaac", last: "Newton", year: 1643, passed: 1727 },
        { first: "Galileo", last: "Galilei", year: 1564, passed: 1642 },
        { first: "Marie", last: "Curie", year: 1867, passed: 1934 },
        { first: "Johannes", last: "Kepler", year: 1571, passed: 1630 },
        { first: "Nicolaus", last: "Copernicus", year: 1473, passed: 1543 },
        { first: "Max", last: "Planck", year: 1858, passed: 1947 },
        { first: "Katherine", last: "Blodgett", year: 1898, passed: 1979 },
        { first: "Ada", last: "Lovelace", year: 1815, passed: 1852 },
        { first: "Sarah E.", last: "Goode", year: 1855, passed: 1905 },
        { first: "Lise", last: "Meitner", year: 1878, passed: 1968 },
        { first: "Hanna", last: "Hammarström", year: 1829, passed: 1909 }
      ];

      const people = [
        "Beck, Glenn",
        "Becker, Carl",
        "Beckett, Samuel",
        "Beddoes, Mick",
        "Beecher, Henry",
        "Beethoven, Ludwig",
        "Begin, Menachem",
        "Belloc, Hilaire",
        "Bellow, Saul",
        "Benchley, Robert",
        "Benenson, Peter",
        "Ben-Gurion, David",
        "Benjamin, Walter",
        "Benn, Tony",
        "Bennington, Chester",
        "Benson, Leana",
        "Bent, Silas",
        "Bentsen, Lloyd",
        "Berger, Ric",
        "Bergman, Ingmar",
        "Berio, Luciano",
        "Berle, Milton",
        "Berlin, Irving",
        "Berne, Eric",
        "Bernhard, Sandra",
        "Berra, Yogi",
        "Berry, Halle",
        "Berry, Wendell",
        "Bethea, Erin",
        "Bevan, Aneurin",
        "Bevel, Ken",
        "Biden, Joseph",
        "Bierce, Ambrose",
        "Biko, Steve",
        "Billings, Josh",
        "Biondo, Frank",
        "Birrell, Augustine",
        "Black Elk",
        "Blair, Robert",
        "Blair, Tony",
        "Blake, William"
      ];
```

## 내가 푼 코드

```jsx
// Array.prototype.filter()
      // 1. Filter the list of inventors for those who were born in the 1500's

      const filtered = inventors.filter(
        (inventor) => inventor.year > 1499 && inventor.year < 1600
      );

      console.log(filtered);

      // Array.prototype.map()
      // 2. Give us an array of the inventors first and last names

      const mapped = inventors.map((inventor) => [
        inventor.first,
        inventor.last
      ]);
      console.log(mapped);

      // Array.prototype.sort()
      // 3. Sort the inventors by birthdate, oldest to youngest

      const sorted = inventors.sort((a, b) =>
        a.year > b.year ? 1 : a.year < b.year ? -1 : 0
      );
      console.log(sorted);

      // Array.prototype.reduce()
      // 4. How many years did all the inventors live all together?

      const reduced = inventors.reduce(
        (total, inventor) => total + (inventor.passed - inventor.year),
        0
      );

      console.log(reduced);

      // 5. Sort the inventors by years lived

      const sortResult = inventors.sort((a, b) => {
        return a.passed - a.year > b.passed - b.year
          ? -1
          : a.passed - a.year < b.passed - b.year
          ? 1
          : 0;
      });

      console.log(sortResult);

      // 6. create a list of Boulevards in Paris that contain 'de' anywhere in the name
      // https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris

      // 7. sort Exercise
      // Sort the people alphabetically by last name

      const sortAlphabet = people.sort((a, b) => a - b);
      console.log(sortAlphabet);

      const alpha = people.sort((lastOne, nextOne) => {
        const [aLast, aFirst] = lastOne.split(", ");
        const [bLast, bFirst] = nextOne.split(", ");
        return aLast > bLast ? 1 : -1;
      });
      console.log(alpha);
      // 8. Reduce Exercise
      // Sum up the instances of each of these
      const data = [
        "car",
        "car",
        "truck",
        "truck",
        "bike",
        "walk",
        "car",
        "van",
        "bike",
        "walk",
        "car",
        "van",
        "car",
        "truck"
      ];

      const dataSum = data.reduce((obj, data) => {
        if (!obj[data]) {
          obj[data] = 0;
        }
        obj[data]++;
        return obj;
      }, {});

      console.log(dataSum);
```

## 답안 코드

```jsx
// Array.prototype.filter()
      // 1. Filter the list of inventors for those who were born in the 1500's
      const fifteen = inventors.filter(
        (inventor) => inventor.year >= 1500 && inventor.year < 1600
      );

      console.table(fifteen);

      // Array.prototype.map()
      // 2. Give us an array of the inventor first and last names
      const fullNames = inventors.map(
        (inventor) => `${inventor.first} ${inventor.last}`
      );
      console.log(fullNames);

      // Array.prototype.sort()
      // 3. Sort the inventors by birthdate, oldest to youngest
      // const ordered = inventors.sort(function(a, b) {
      //   if(a.year > b.year) {
      //     return 1;
      //   } else {
      //     return -1;
      //   }
      // });

      const ordered = inventors.sort((a, b) => (a.year > b.year ? 1 : -1));
      console.table(ordered);

      // Array.prototype.reduce()
      // 4. How many years did all the inventors live?
      const totalYears = inventors.reduce((total, inventor) => {
        return total + (inventor.passed - inventor.year);
      }, 0);

      console.log(totalYears);

      // 5. Sort the inventors by years lived
      const oldest = inventors.sort(function (a, b) {
        const lastInventor = a.passed - a.year;
        const nextInventor = b.passed - b.year;
        return lastInventor > nextInventor ? -1 : 1;
      });
      console.table(oldest);

      // 6. create a list of Boulevards in Paris that contain 'de' anywhere in the name
      // https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris

      // const category = document.querySelector('.mw-category');
      // const links = Array.from(category.querySelectorAll('a'));
      // const de = links
      //             .map(link => link.textContent)
      //             .filter(streetName => streetName.includes('de'));

      // 7. sort Exercise
      // Sort the people alphabetically by last name
      const alpha = people.sort((lastOne, nextOne) => {
        const [aLast, aFirst] = lastOne.split(", ");
        const [bLast, bFirst] = nextOne.split(", ");
        return aLast > bLast ? 1 : -1;
      });
      console.log(alpha);

      // 8. Reduce Exercise
      // Sum up the instances of each of these
      const data = [
        "car",
        "car",
        "truck",
        "truck",
        "bike",
        "walk",
        "car",
        "van",
        "bike",
        "walk",
        "car",
        "van",
        "car",
        "truck",
        "pogostick"
      ];

      const transportation = data.reduce(function (obj, item) {
				// obj에 item이 없으면
        if (!obj[item]) {
				// item : 0 으로 만듬
          obj[item] = 0;
        }
				// item : 0 에서 시작해서 숫자를 하나씩 올림
        obj[item]++;
        return obj;
      }, {});

      console.log(transportation);
```

- 마지막 문제를 제외하고는 다 해결했는데 마지막 문제는 방법이 생각나지 않아서 답안을 보고 공부를 했다.
- 7번을 제외한 나머지의 답은 전부 일치했고, 다만 7번 같은 경우에는 답안에서는 aLast만 비교를 했는데 오히려 내 방법이 맞다는 생각이 든다.
