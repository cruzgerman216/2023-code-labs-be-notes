## Setup

-   Create angular project

```
 ng new crimson-university-client --no-strict
```

```
? Would you like to add Angular routing? Yes
? Which stylesheet format would you like to use? SCSS
```

Paste CDN links to include Bootstrap 5 in the project

**src/index.html**

```html
<head>
    <meta charset="utf-8" />
    <title>CrimsonUniversityClient</title>
    <base href="/" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />
    <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
        rel="stylesheet"
        integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
        crossorigin="anonymous"
    />
    <script
        src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM"
        crossorigin="anonymous"
    ></script>
</head>
```

## Login

```
ng g c auth/login
```

**src/app/app-routing.module.ts**

```js
const routes: Routes = [
    {
        path: "login",
        component: LoginComponent,
    },

    {
        path: "",
        redirectTo: "login",
        pathMatch: "full",
    },
    {
        path: "**",
        redirectTo: "login",
    },
];
```

**src/app/app.component.html**

```html
<div class="container">
    <router-outlet></router-outlet>
</div>
```

**src/styles.scss**

```scss
/* You can add global styles to this file, and also import other style files */
* {
    box-sizing: border-box;
    font-family: "Merriweather Sans", sans-serif;
}

body {
    background-color: #dc143c;
}
```

**src/app/auth/login/login.component.html**

```html
<h1 class="text-center mt-5 text-white">Login</h1>

<form id="form">
    <p>
        Student logins are provided via the university. If not received, be sure
        to contact administration.
    </p>

    <div class="form-group">
        <label for="email">Your Email</label>
        <br />
        <div class="input-group">
            <input type="email" id="email" placeholder="Enter Your Email" />
        </div>
    </div>

    <div class="form-group">
        <label for="password">Your Password</label>
        <br />
        <div class="input-group">
            <input
                type="password"
                id="password"
                placeholder="Enter Your Password"
            />
        </div>
    </div>

    <button type="submit" class="btn btn-default text-white">Login</button>
</form>
```

```scss
#form {
    color: white;
    background-color: #dc143c;
    border-radius: 5px;

    width: 400px;
    padding: 40px;
    margin: 100px auto;

    box-shadow: -1px 3px 18px 0px rgba(0, 0, 0, 0.75);

    p {
        font-size: 0.9em;
    }

    button {
        width: 100%;
        text-align: center;
        margin-top: 20px;
        border: 1px solid rgba(0, 0, 0, 0.4);
    }

    .form-group {
        margin: 15px auto;

        label {
            font-weight: bold;
            font-size: 0.9em;
        }

        .input-group {
            border-radius: 5px;
            box-shadow: -1px 3px 18px 0px rgba(0, 0, 0, 0.35);
            input {
                padding-left: 10px;
            }
        }

        input {
            padding: 3px;
            width: 100%;
            border: none;
            border-radius: 0 5px 5px 0;
        }
    }
}
```

## Admin View

**terminal**

```
 ng g m admin
```

**src/app/app-routing.module.ts**

```js
const routes: Routes = [
    {
        path: "login",
        component: LoginComponent,
    },
    {
        path: "admin",
        loadChildren: () =>
            import("./admin/admin.module").then((m) => m.AdminModule),
    },
    {
        path: "",
        redirectTo: "login",
        pathMatch: "full",
    },
    {
        path: "**",
        redirectTo: "login",
    },
];
```

**terminal**

```
ng g m admin/admin-routing
```

**src/app/admin/admin-routing.module.ts**

```js
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { AdminDashboardComponent } from "./admin-dashboard/admin-dashboard.component";

const routes: Routes = [
    {
        path: "dashboard",
        component: AdminDashboardComponent,
    },
    {
        path: "**",
        pathMatch: "full",
        redirectTo: "",
    },
];

@NgModule({
    imports: [RouterModule.forChild(routes)],
    exports: [RouterModule],
})
export class AdminRoutingModule {}
```

-   Create a simple view for admin panel

**src/app/admin/admin-dashboard/admin-dashboard.component.html**

```html
<h1 class="text-center text-white">Admin Panel</h1>
```

## Logging as admin

-   Open crimson-university-api and run the server in the background

-   import ReactiveForms Module

**src/app/app.module.ts**

```js
imports: [BrowserModule, AppRoutingModule, ReactiveFormsModule];
```

**src/app/auth/login/login.component.ts**

```js
loginForm = new FormGroup({
    username: new FormControl("", [Validators.required]),
    password: new FormControl("", [Validators.required]),
});
```

**src/app/auth/login/login.component.html**

```html
<h1 class="text-center mt-5 text-white">Login</h1>

<form id="form" [formGroup]="loginForm" (ngSubmit)="onLogin()">
    <p>
        Student logins are provided via the university. If not received, be sure
        to contact administration.
    </p>

    <div class="form-group">
        <label for="email">Your Email</label>
        <br />
        <div class="input-group">
            <input
                type="email"
                id="email"
                placeholder="Enter Your Email"
                formControlName="email"
            />
        </div>
    </div>

    <div class="form-group">
        <label for="password">Your Password</label>
        <br />
        <div class="input-group">
            <input
                type="text"
                id="password"
                placeholder="Enter Your Password"
                formControlName="password"
            />
        </div>
    </div>

    <button type="submit" class="btn btn-default text-white">Login</button>
</form>
```

**src/app/auth/login/login.component.ts**

```js
  onLogin(){

  }
```

```
ng g s auth/auth
```

-   Import Http Client Module

**src/app/app.module.ts**

```js
import { HttpClientModule } from '@angular/common/http';
.
.
.
.
  imports: [
    BrowserModule,
    AppRoutingModule,
    ReactiveFormsModule,
    HttpClientModule,
  ],
```

**src/app/auth/auth.service.ts**

```js
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class AuthService {
  constructor(private http: HttpClient) {}

  login(user) {
    return this.http.post('http://localhost:3000/api/v1/users/login', user).subscribe({
      next: (res) => {
        console.log(res);
      },
    });
  }
}
```

**src/app/auth/login/login.component.ts**

```js
export class LoginComponent implements OnInit {
  loginForm = new FormGroup({
    email: new FormControl('', [Validators.required]),
    password: new FormControl('', [Validators.required]),
  });
  constructor(private authService:AuthService) {}

  ngOnInit(): void {}

  onLogin(){
    this.authService.login(this.loginForm.value);
  }
}
```

-   Login as an admin and get valid response

## Navigate admin to route

In crimson-university-api, let's send back user roles

**app/models/user.rb**

```rb
  def get_roles
    roles.map { |role| role["slug"] }
  end
```

**app/blueprints/user_blueprint.rb**

```rb
class UserBlueprint < Blueprinter::Base
  identifier :id
  fields :first_name, :last_name, :name, :email, :get_roles
```

In crimson-university-client,
**src/app/auth/auth.service.ts**

```js
  login(user) {
    return this.http
      .post('http://localhost:3000/api/v1/users/login', user)
      .subscribe({
        next: (res: any) => {
          // successful?
          if (res.success) {
            // admin?
            if (res.payload.user.get_roles.includes('admin')) {
              // navigate to admin dashboard
              this.route.navigate(['/admin/dashboard']);
            }
          }
        },
      });
  }
```

## Admin Panel - See all Users

```
ng g c admin/admin-users
```

-   Make sure every other path redirects to /dashboard/users

**src/app/admin/admin-routing.module.ts**

```js
const routes: Routes = [
    {
        path: "dashboard",
        component: AdminDashboardComponent,
        children: [
            {
                path: "users",
                component: AdminUsersComponent,
            },
        ],
    },
    {
        path: "**",
        pathMatch: "full",
        redirectTo: "dashboard/users",
    },
];
```

```js
import { HttpClient } from '@angular/common/http';
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-admin-users',
  templateUrl: './admin-users.component.html',
  styleUrls: ['./admin-users.component.scss'],
})
export class AdminUsersComponent implements OnInit {
  users:any = null;

  constructor(private http: HttpClient) {}

  ngOnInit(): void {
    this.http
      .get('http://localhost:3000/api/v1/users/list')
      .subscribe((res: any) => {
        if(res.success){
          this.users = res.payload
        }
      });
  }
}
```

In your API, define a list route 

**routes.rb**
```rb
      namespace :users do
        post :login
        delete :logout
        get :me
        post :create
        get :list
      end
```

**users_controller.rb**
```rb
      def list 
        render_success(payload: UserBlueprint.render_as_hash(User.all), status: 200)
      end
```

In client, 

**src/app/admin/admin-users/admin-users.component.html**

```html
<table class="table bg-white text-center" *ngIf="users">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">First</th>
      <th scope="col">Last</th>
      <th scope="col">email</th>
      <th scope="col">Roles</th>
      <th scope="col">Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let user of users">
      <th scope="row">{{ user.id }}</th>
      <td>{{ user.first_name }}</td>
      <td>{{ user.last_name }}</td>
      <td>{{ user.email }}</td>
      <td>
        <span *ngFor="let role of user.get_roles">{{ role }} </span>
      </td>
      <td>
        <button class="btn btn-secondary">Edit</button>
        <button class="btn btn-danger text-white">Delete</button>
        <button class="btn btn-primary text-white">View</button>
      </td>
    </tr>
  </tbody>
</table>
```
