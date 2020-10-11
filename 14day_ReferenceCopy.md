# 1일 1프로젝트 (14일차 Reference vs Copy)

```jsx
// 변수
      // 값만 복사했기 때문에 같이 바뀌지 않는다.
      let age = 100;
      let age2 = age;
      console.log(age, age2); // 100 , 100
      age = 200;
      console.log(age, age2); // 100 , 200

      let name = "Wes";
      let name2 = name;
      console.log(name, name2); // Wes , Wes
      name = "wesley";
      console.log(name, name2); // wesley , Wes

      // 배열
      const players = ["Wes", "Sarah", "Ryan", "Poppy"];
      const team = players;

      // 값을 참조하고 있기 때문에 같이 바뀐다.
      team[3] = "Lux";
      console.log(players, team);
      // ["Wes", "Sarah", "Ryan", "Lux"]
      // ["Wes", "Sarah", "Ryan", "Lux"]

      // 값만 복사하고 같이 참조하지 않는 방법들
      // 값을 바꿔도 같이 바뀌지 않는다.
      // 1
      const team2 = players.slice();
      // 2
      const team3 = [].concat(players);
      // 3
      const team4 = [...players];
      // 4
      const team5 = Array.from(players);

      // 객체
      const person = {
        name: "Wes Bos",
        age: 80
      };

      // 값을 참조하고 있기 때문에 같이 바뀐다.
      const captain = person;
      captain.number = 99;
      console.log(person.number); // 99

      // 값을 같이 참조해서 같이 바뀌지 않게 하는 방법
      // 1
      const cap2 = Object.assign({}, person, { number: 80, age: 12 });
      console.log(cap2); // {name: "Wes Bos", age: 12, number : 80}
      console.log(person); // {name: "Wes Bos", age: 80, number : 99}

      // 2
      const cap3 = { ...person };

      const wes = {
        name: "Wes",
        age: 100,
        social: {
          twitter: "@wesbos",
          facebook: "wesbos.developer"
        }
      };

      console.log(wes);

      const dev = Object.assign({}, wes);
      // name,age는 같이 바뀌지 않지만, social 내부의 twitter,facebook을 수정하면 같이 바뀐다.

      // 3
      // social 내부까지도 같이 바뀌지 않는다.
      const dev2 = JSON.parse(JSON.stringify(wes));
```
