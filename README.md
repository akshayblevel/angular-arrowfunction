# angular-arrowfunction

employee.ts

```js
export interface IEmployee {
  id: number;
  code: string;
  name: string;
  salary: number;
}
```

employee-component.component.ts

```js
import { Component, OnInit } from '@angular/core';
import { IEmployee } from './employee';

@Component({
  selector: 'app-employee-component',
  templateUrl: './employee-component.component.html',
  styleUrls: ['./employee-component.component.css']
})
export class EmployeeComponentComponent implements OnInit {
  constructor() {}

  ngOnInit() {
    this.listFilter = 'Patel';
  }

  private _listFilter: string = '';

  get listFilter(): string {
    return this._listFilter;
  }

  set listFilter(value: string) {
    this._listFilter = value;
    console.log('In Setter:', value);
    this.filteredEmployees = this.performFilter(value);
  }

  filteredEmployees: IEmployee[] = [];
  employees: IEmployee[] = [
    {
      id: 1,
      code: 'VOD1410',
      name: 'Akshay Patel',
      salary: 3000
    },
    {
      id: 2,
      code: 'VOD1710',
      name: 'Panth Patel',
      salary: 1500
    },
    {
      id: 2,
      code: 'VOD0408',
      name: 'Satish Patel',
      salary: 5000
    }
  ];

  performFilter(filterBy: string): IEmployee[] {
    filterBy = filterBy.toLocaleLowerCase();
    return this.employees.filter((employee: IEmployee) =>
      employee.name.toLocaleLowerCase().includes(filterBy)
    );
  }
}
```
employee-component.component.html

```html
<div>
  <div>
    <input type="text" [(ngModel)]="listFilter" />
  </div>
  <br />
  <div>
    Filter By: {{listFilter}}
  </div>
  <div>
    <table>
      <thead>
        <td>Id</td>
        <td>Code</td>
        <td>Name</td>
        <td>Salary</td>
      </thead>
      <tr *ngFor="let employee of filteredEmployees">
        <td>{{employee.id}}</td>
        <td>{{employee.code}}</td>
        <td>{{employee.name}}</td>
        <td>{{employee.salary}}</td>
      </tr>
    </table>
  </div>
</div>
```

app.module.ts

```js
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { employeeComponentComponent } from './employee-component/employee-component.component';

@NgModule({
  imports: [BrowserModule, FormsModule],
  declarations: [AppComponent, employeeComponentComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

app.component.html

```html
<app-employee-component></app-employee-component>
```


