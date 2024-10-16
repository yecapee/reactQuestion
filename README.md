# react-question

## 1

### Q1
```js
function sortUserName(users) {
  return users.sort((a, b) => {
    const nameA = (`${a.firstName}${a.lastName}${a.customerID}`).toLowerCase();
    const nameB = (`${b.firstName}${b.lastName}${b.customerID}`).toLowerCase();
    return nameA.localeCompare(nameB);
  });
}
```

### Q2
```js
function sortByType(users) {
  const professionOrder = {
    systemAnalytics: 1,
    engineer: 2,
    productOwner: 3,
    freelancer: 4,
    student: 5,
  };

  return users.sort((a, b) => {
    return professionOrder[a.profession] - professionOrder[b.profession];
  });
}
```

## 2
```CSS
  .container .shop-list li.item:first-child {
      /* Explain why does this color not works, and how to fix make it work on 1st list */
      color: blue;
  }

  /* Write styling make every other line give background color to next one */
  .container .shop-list li.item:nth-child(even){
      color: gray;
  }
```


### 3
```js
function getUniqueNumber(items) {
  return [...new Set(items)];
}
```

### 4

#### Interface
Interface 是一個定義物件結構的規範,用來定義物件應該有哪些屬性和方法,但不會實現具體的邏輯
Interface 有助於保持代碼的一致性和可讀性

**使用場景**
>在多個類之間共享結構時，可以用 Interface 確保結構相同。
>定義 API 返回的物件結構或函數的參數，確保代碼符合預期的輸入和輸出。
```ts
interface User {
  firstName: string;
  lastName: string;
  age: number;
  isAdmin: boolean;
}

function printUser(user: User): void {
  console.log(`${user.firstName} ${user.lastName}, Age: ${user.age}`);
}
```

#### Enum
Enum是TypeScript的數據類型, 用於定義一組命名的常數, 可以提高代碼的可讀性, 讓代碼更加語義化
Enum可以有number或string

**使用場景**
>當有一組固定的常數值（如狀態、類型）時, 用 Enum 來代表它們會讓代碼更容易理解和維護
>使用枚舉可以防止使用錯誤的常量值

```ts
enum Role {
  Admin = "Admin",
  User = "User",
  Guest = "Guest"
}


function checkRole(role: Role): void {
  if (role === Role.Admin) {
    console.log("Hello Admin");
  } else if (role === Role.User) {
    console.log("Hello User");
  } else {
    console.log("Hello Guest");
  }
}

// 使用Enum
checkRole(Role.Admin);  // Output: "Hello Admin"
checkRole(Role.Guest);  // Output: "Hello Guest"
```

### 5
this.state在這個週期都會維持同一個值,所以重複調用只是一直針對目前週期的狀態+1, 要累加可以使用setState回傳的prevState參考
```jsx
import React, { Component } from 'react';

class Count extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.handleAddCount = this.handleAddCount.bind(this);
  }

  handleAddCount() {
    this.setState((prevState) => ({ count: prevState.count + 1 }));
    this.setState((prevState) => ({ count: prevState.count + 1 }));
    this.setState((prevState) => ({ count: prevState.count + 1 }));
  }

  render() {
    return (
      <div>
        <h2>{this.state.count}</h2>
        <button onClick={this.handleAddCount}>Add</button>
      </div>
    );
  }
}

export default Count;
```

### 6
```jsx
import React, { Component } from 'react';

function debounce(func, delay) {
  let timeout;
  return function (...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), delay);
  };
}

var SearchBox = React.createClass({
  render: function() {
    return <input type="search" name="p" onChange={this.handleOnChange}
    />;
  },

  handleOnChange: () => {
    let timeout;
    return (event) => {
      clearTimeout(timeout);
      timeout = setTimeout((event) => {
        setSearchValue(event.target.value);
        console.log('AJAX请求:', event.target.value);
      }, 500);
    }
  }
});

```
