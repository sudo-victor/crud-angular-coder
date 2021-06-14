# Angular 9 - curso Cod3r

## O que é Angular?

Um framework Javascript desenvolvido pelo Google para criação de aplicações web SPA baseada em componentes.

## Command Line Interface

É utilizado a cli do angular para criar o projeto:

- `npm i -g @angular/cli`
- `ng new minha-app`

## Typescript

Linguagem criada pela Microsoft, onde ela é compilada para javascript. Um superset do Javascript onde é adicionado novas funcionalidades como a tipagem e POO.

## Árvore de Componentes

O AppComponent é o component pai onde os outros compoentes irão ser seus filhos:

AppComponent > Header > Nav
AppComponent > Content > ContentTitle

## Inicialização do APP

O primeiro arquivo que será chamado para começar o app:

- main.ts > AppModule > AppComponent

## O que é um componente?

Um trexo de código que representa uma parte da tela, HTML, CSS e TS.
Cada componente terá sua estrutura, desse forma:

- home.component.css
- home.component.html
- home.component.ts

## Anatomia do Módulo

Dentro de um módulo há 5 atributos, sendo eles:

- Declarations: Components, Diretivas e Pipes;
- Exports: Components, Diretivas e Pipes;
- Imports: Module A, Module B e Module C;
- Providers: Service A, Service B e Service C;
- Bootstrap: App Component;

## Elementos do Angular

Os Compoenentes:

- HTML;
- CSS;
- Typescript.

## Attribute Directives

Altera a aparência e o comportamento de um elemento, componente ou outra diretiva. Tem como vincular um comportamento a um elemento.

Exemplo:

- Diretiva:

```javascript
@Directive({
  selector: "[appRed]",
})
export class RedDirective {
  constructor(el: ElementRed) {
    el.nativeElement.style.color = "#e35e6b";
  }
}
```

- HTML:

```html
<i class="material-icons v-middle" appRed> favorite </i>
```

## Strutural Directives

Altera o layout adicionando e removendo elementos da DOM.

Exemplo:

- Diretiva:

```javascript
@Directive({
  selector: "[appRed]",
})
export class RedDirective {
  constructor(el: ElementRed) {
    el.nativeElement.style.color = "#e35e6b";
  }
}
```

- HTML:

```html
<form *ngIf="product" class="product-form"></form>
```

```html
<li *ngFor="let product of products" class="product-form">
  {{ product.name }}
</li>
```

## Property Binding

Usar variaveis do component no html a partir do componente typescript.

- HTML:

```html
<table [dataSource]="products"></table>
```

- Typescript:

```Typescript
@Component({
  selector: 'app-product-read',
  tempalteUrl: './product-read.component.html',
  styleUrls: ['./product-read.component.css']
})
export class ProductReadComponent implements OnInit {
  products: Product[];
}
```

## Event Binding

Usar funcoes dentro do html a partir do componente typescript

- HTML:

```html
<button mat-raised-button (click)="createProduct()" color="primary">
  Salvar
</button>
```

- Typescript:

```Typescript
@Component({
  selector: 'app-product-create',
  tempalteUrl: './product-create.component.html',
  styleUrls: ['./product-create.component.css']
})
export class ProductCreateComponent implements OnInit {

  createProduct(): void {
    // ...
  }

}
```

## One Way Data Binding

A alteração do property binding só é feita do lado do typescrypt para o html. Ou seja, quando um atributo de uma classe componente mudar seu valor o html que usa esse atributo tbm será mudado, mas não o contrário.

- HTML:

```html
<input [value]="nome" />
```

- Typescript:

```Typescript
nome: string;
```

## Two Way Data Binding

A alteração do property no typescript irá atualizar no html e se mudar no html irá atualizar no typescript tbm.

- HTML:

```html
<input [(ngModel)]="nome" />
```

- Typescript:

```Typescript
nome: string;
```

## Angular Router

/home -> Comp.Home
/produto -> Comp.Produto
/usuario -> Comp.Usuario

Router Outlet -> Componente que seleciona o componente certo.

Exemplo:

```html
<a routerLink="/products"> Produtos </a>
```

```typescript
const routes: Routes = [
  {
    path: "products",
    component: ProductCrudComponent,
  },
  {
    path: "products/create",
    component: ProductCreateComponent,
  },
];
```

## Angular Pipes

Exemplo:

```html
<p>O vencimento e {{ produto.vencimento | date: 'fullDate' | uppercase }}</p>

<td mat-cell *matCellDef="let product">
  {{ product.price | currency: 'BRL' }}
</td>
```

## Programação Reativa

### O Padrão Observer

Padrão orientado a Evento.

Subject -> Quem tem a capacidade de monitorar e detectar quando um evento acontece.
Observer -> Os códigos q estão interessadas em determinado evento.

```typescript
criarNoBackend(produto: Produto): Observable<Produto> {
  return this.http.post<Produto>(this.url, produto);
}

criarProduto(): void {
  this.criarNoBackend(this.produto).subscribe(() => {
    this.exibirMensagem("Salvo com sucesso!");
  })
}
```

## O que são Services?

São classes que têm como principal objetivo organizar e compartilhar métodos e dados entre componentes

```typescript
// ng g s services/product

@Injectable({
  providedIn: "root",
})
export class ProductService {
  // ...
}
```

### Injeção de Dependência

É um padrão no qual a classe recebe as dependências de uma fonte externa ao invés de criar por conta própria.

```typescript
class Carro {
  motor: Motor;

  constructor() {
    this.motor = new Motor();
  }
}

class Motor {}
```

Refatorado:

```typescript
class Carro {
  motor: Motor;

  constructor(motor: Motor) {
    this.motor = motor;
  }
}

class Motor {
  cilindrada: number;

  constructor(cilindrada: number) {
    this.cilindrada = cilindrada;
  }
}
```

Services são singletons dentro do escopo de um injector: ModuleInjector, ElementInjector.
