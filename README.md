<p align="center"><img src="https://raw.githubusercontent.com/laravel/art/master/laravel-logo.png" width="400"></p>

<p align="center">Small study documentation of the PHP <a href="https://laravel.com">👉 Laravel framework 👈</a>, developing an ecommerce platform.</p>

<p align="center">
    <a href="#">
        <img alt="Passing" src="https://img.shields.io/circleci/build/github/MagicalStrangeQuark/ecommerce-laravel">
    </a>
    <a href="https://opensource.org/licenses/MIT">
        <img alt="License" src="https://img.shields.io/badge/License-MIT-yellow.svg">
    </a>
    <a href="#">
        <img alt="License" src="https://img.shields.io/github/languages/count/MagicalStrangeQuark/ecommerce-laravel">
    </a>
    <a href="#">
        <img alt="License" src="https://img.shields.io/github/last-commit/MagicalStrangeQuark/ecommerce-laravel">
    </a>
    <a href="#">
        <img alt="License" src="https://img.shields.io/github/followers/MagicalStrangeQuark?style=social">
    </a>
</p>

<h2 align="center">Configuring the machine to start the application</h2>

🔏 Installing Apache

```bash
    sudo pacman -S apache
```

🔏  Installation of tools that will be needed later

```bash
    sudo pacman -S curl git unzip
```

🔏  Installing Composer

```bash
    sudo su
```

```bash
    curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

🔏 Installing the  <a href="https://addons.mozilla.org/pt-BR/firefox/addon/restclient">👉 RESTClient 👈</a> extension

🪔 `To test the use of API's and other features within our application, it is recommended to use a tool to perform the request simulation.`

<h2 align="center">Starting a new Laravel project</h2>

<h3 align="center">🐉 Create a new project</h3>

```bash
    composer create-project --prefer-dist laravel/laravel some-project-name
```

<h3 align="center">🐲 Installation of project dependencies</h3

```bash
    composer install
```

<h2 align="center">Visual Studio Code Extensions</h2>

🦝 <a href="https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv">🌖 DotENV 🌘</a>

🦝 <a href="https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel5-snippets">💐 Laravel Snippets 🪐</a>

🦝 <a href="https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-blade">🌾 Laravel Blade Snippets 🌚 </a>

🦝 <a href="https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client">💫 PHP Intelephense 🌻</a>

<h2 align="center">Run the project from the current project</h2>

```bash
    git clone https://github.com/MagicalStrangeQuark/ecommerce-laravel.git
```

<h2 align="center">Create and configure the database (MariaDB)</h2>

```sql
    CREATE DATABASE laravel
```

```sql
    CREATE USER 'laravel'@'localhost' IDENTIFIED BY 'P@ssw0rd'
```

```sql
    GRANT ALL PRIVILEGES ON * . * TO 'laravel'@'localhost'
```

```sql
    FLUSH PRIVILEGES
```

<h3 align="center">Configure the .env file</h3>

```bash
    cd ecommerce-laravel && cp .env.example .env && php artisan key:generate`
```

```bash
    php artisan config:clear && php artisan cache:clear && php artisan config:cache
```

```bash
    composer install && composer update
```

```bash
    npm install && npm audit fix && npm run watch
```

```bash
    sudo systemctl start mariadb
```

```bash
    php artisan migrate:fresh --seed
```

```bash
    php artisan storage:link
```

```bash
    php artisan serve
```

```bash
    firefox http://127.0.0.1:8000
```

<h2 align="center">Form Validation</h2>

No objeto request é possível acessar o método validate, bastando inserir um array associativo com a chave contendo o name do campo e o valor required, sendo
validado se existe conteúdo. No exemplo abaixo, estamos verificando se o campo color foi informado:

```php
    $request->validate([
        "color" => "required"
    ]);
```

Para inserir mais validações simultaneamente, basta concatenar usando o pipe. No exemplo abaixo, não queremos mais de 10 caracteres no mesmo campo color.

```php
    $request->validate([
        "color" => "required|max:10"
    ]);
```

Para validação única, basta informar `unique:<nome-da-tabela>`, para o campo desejado, o seguinte exemplo pode ser útil:

```php
    $request->validate([
        "color" => "required|unique:colors",
        "hexadecimal" => "required|min:6|max:6|unique:colors,hexadecimal"
    ]);
```

Exemplo de validação de email:

```php
    $request->validate([
        "email" => "required|email",
    ]);
```

Para utilização de mensagens não genéricas, pode-se usar uma chave com o nome da validação, com a mensagem, sendo passsado o placeholder `:attribute`. Exemplo:

```php
    $request->validate([
            "color" => "required|unique:colors",
            "hexadecimal" => "required|min:6|max:6|unique:colors"
        ],[
            "hexadecimal.min" => "O hexadecimal deve conter seis caracteres",
            "unique" => "O atributo :attribute deve ser único"
    ]);
```

Para criação de mensagens abaixo do campo com erro / sucesso, o Laravel possui, dentro do objeto $errors, um método chamado `has()`, em que é passado o name, sendo retornado um booleano indicando se aquele campo contém erros.

<h2 align="center">Helpers</h2>

Para realizar a criação de um arquivo helper, criaremos um arquivo chamado `Html.php`, dentro do diretório `app/Helpers`.

No arquivo `composer.json`, inserir o código abaixo dentro da chave autoload e rodar o comando `composer dump-autoload`.

```php
    "files": [
        "app/Helpers/Html.php"
    ]
```

Adicionar, no diretório config, no arquivo app.php, em aliases, a linha `'Helper' => App\Helpers\Helper::class`

<h2 align="center">Routes</h2>

Listando todas as rotas do meu projeto

```bash
    php artisan route:list
```

Criamos, nesse exemplo, uma rota para a marca em que é passada uma descrição e um valor e essa retorna a impressão dessa descrição tantas vezes.

É realiza uma validação para o nome, sendo permitido apenas caracteres alfanuméricos; e para o número, sendo apenas naturais.

```bash
    http://127.0.0.1:8000/app/Marca/Lat1ex/5
```

```bash
    Route::get('/Marca/{name?}/{n}', function (string $name = '', int $n = 0) {
        for ($i = 0; $i < $n; $i++) {
            echo "<p>Marca: {$name}</p>";
        }
    })->where('name', '[A-Za-z\d]+')->where('n', '[0-9]+')->name('app.marca');
```

Redirecionada para a rota nomeada `app` (Name)

```bash
    return redirect()->route('app');
```

Redireciona para ação `\app` (URI)

```bash
    return redirect('/app');
```

<h6 align="center">Documentação oficial</h6>

<https://laravel.com/docs/master/routing>

Testando uma requisição POST:

Adicionar a rota POST à lista de exceções da classe VerifyCsrfToken.

Através do RestClient, solicitar a url desejada. Por exemplo, <http://127.0.0.1:8000/exit>.
  
[Unicode Special Character](http://niviotec.blogspot.com/2015/12/codigos-unicode-para-caracteres.html)

<h2 align="center">Controllers</h2>

Criar um controlador para o gerenciamento de marcas dentro do nosso sistema

```php
    php artisan make:controller MarcaController --resource
```

O objeto $request possui um método para a exibição do conteúdo que recebemos do formulário

```php
    $request->all()
```

<h3 align="center">CSS</h3>

Criarmos um arquivo simple-sidebar.css.

Adicionando CSS ao projeto: Inserir o arquivo .css na pasta public/css

Referenciar o arquivo com o seguinte código:

```html
    <link href="{{ asset('css/simple-sidebar.css') }}" rel="stylesheet">
```

<h3 align="center">Componentes</h3>

Dentro do diretório resources/views, criar uma pasta chamada component.

Criamos o arquivo `list.blade.php` e inserimos um pequeno código html.

```html
    <div style="border: 1px solid red">
        <h1>Component</h1>
        <p align="center"> Lista Component</p>
    </div>
```

Assim, chamamos nosso componente da seguinte forma:

```php
    @component('components.list')

    @endcomponent
```

É possível passar conteúdo html para o componente, que será armazenado numa variável chamada $slot, da seguinte forma

```php
    @component('components.list')
        <h1>Conteúdo html sendo inserido no componente</h1>
    @endcomponent
```

O conteúdo é recuperado então da seguinte forma

```html
    <div style="border: 1px solid red">
        <h1>Component</h1>
        <p align="center"> Lista Component</p>
        <p>{{ $slot }}</p>
    </div>
```

Uma segunda forma é passar os parâmetros através de um array associativo.

```php
    @component('components.list', ['msg' => 'Conteúdo html sendo inserido no componente'])

    @endcomponent
```

E recuperar o conteúdo através da variável criada a partir do índice.

```html
    <div style="border: 1px solid red">
        <h1>Component</h1>
        <p align="center"> Lista Component</p>
        <p align="center">{{ $msg }}</p>
    </div>
```

Uma terceira forma de usar componentes é através da declaração dos mesmos. Na classe AppServiceProvider, inserimos a declaração do componente, através da sintaxe `Blade::component("<directory>", "<component-name>")` dentro do método boot();

Após isso incluímos a classe, inserindo a declaração `use Illuminate\Support\Facades\Blade`

Na view, chamamos esse componente usando a seguinte sintaxe

```php
    @<component-name>(['<variable>' => '<string>'])

    @end<component-name>
```

<h3 align="center">Adicionando Bootstrap 4</h3>

No terminal, no diretório do nosso projeto, rodar os seguintes comandos:

```php
    composer require laravel/ui

    php artisan ui bootstrap

    npm install && npm run dev
```

<h4 align="center">FPDF</h4>

```php
    composer require setasign/fpdf
```

<h2 align="center">Models</h2>

<h3 align="center">Configuração do Banco de Dados e das Migrações</h3>

```php
    1. Realizar a instalação do SGBD mysql

    2. Habilitar o driver do mysql extension=pdo_mysql

    3. Verificar se o driver está habilitado corretamente, rodando o seguinte comando:

        php -r "echo defined('PDO::ATTR_DRIVER_NAME');";

    4. Rodar as migrações e seeds `php artisan migrate:fresh --seed`
```

<h3>Criação de uma migração</h3>

Criação de uma tabela chamada colors

```php
    php artisan make:migration create_colors_table
```

Adicionar um campo chamado color a uma tabela chamada chemical_elements

```php
    php artisan make:migration add_color_to_chemical_elements`
```

Criação de um relacionamento muitos para muitos

```php
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('products_categories', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->unsignedBigInteger('product_id');
            $table->foreign('product_id')->references('id')->on('products');
            $table->unsignedBigInteger('category_id');
            $table->foreign('category_id')->references('id')->on('categories');
            $table->softDeletes();
            $table->timestamps();
        });
    }
```

```php
    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('products_categories');
    }
```

Criação de um modelo para a tabela colors

```php
    php artisan make:model Color
```

Criação de um registro para a color, através do tinker

```php
    php artisan tinker;

    use App\Color;

    $colors = Color::create(['color' => 'Black', 'hexadecimal' => '000000']);
```

Listagem de todos os registros para a color, através do tinker

```php
    use \App\Color;
        
    php Color::all();
```

Número de registros

```php
    use App\Color;

    Color::count();
```

Select usando where

```php
    use App\Color;
```

```php
    Color::where('id', '>=', 2)->first();
```

```php
    Color::where('id', 2)->get();
```

```php
    Color::whereBetween('id', [1,2])->get();
```

```php
    Color::whereNotBetween('id', [2, 3])->get();
```

```php
    Color::whereIn('id', [2, 3])->get();
```

```php
    Color::whereNotIn('id', [2, 3])->get();
```

```php
    Color::where('color', 'like', '%k')->get();
```

As duas consultas abaixo são equivalentes

```php
    Color::where('color', 'like', 'B%')->orWhere('id', '>=', 7)->get();

    Color::where(function($query){$query->where('color', 'like', 'B%')->orWhere('id', '>=', 7);})->get();

    Color::where(function($query){
            $query->where('color', 'like', 'B%')->orWhere('id', '>=', 7);
        })->where(function($query) {
                $query->where('color', 'like', '%e%')
                ->where('id', '>=', 10 );
            })->get();

    Color::where('id', '>', '1')->orderBy('color', 'ASC')->get();

    Color::where('id', '>', '1')->get()->pluck('id')->sum();
```

Set Custom Primary Key

No model, incluir a linha `protected $primaryKey = 'id'`

Atualizar um campo

```php
    use App\Color;

    $Color = Color::find(2);
    $Color->color = "Black";
    $Color->save();
```

```php
    Color::find(6)->update(['color' => 'Green']);
```

Soft Delete

    No model, incluir a trait, usando `use SoftDeletes` e incluir o namespace da mesma, com `use Illuminate\Database\Eloquent\SoftDeletes`

    Inclusão do campo, através da seguinte migração `$table->softDeletes()`

Listar incluive os registros deletados

```php
    use App\Color;

    Color::withTrashed->get();
```

Verificar se um registro em particular, no caso, o id de número 2, está deletado

```php
    use App\Color;

    Color::withTrashed()->find(2)->trashed();
```

Excluir um registro de id igual a 3 com SoftDelete

```php
    use App\Color;

    Color::find(5)->forceDelete();
```

<h2 align="center">Views (Blade)</h2>

<h3>Condicional</h3>

```php
    @if
        <code>
    @else
        <code>
    @endif
```

<h3>Foreach</h3>

```php
    @foreach
        <code>
    @endforeach
```

O framework disponibiliza um objeto chamado $loop, que possibilita obter o primeiro e último elemento do laço de repetição.
 
Reference: <https://tutsforweb.com/loop-variable-foreach-blade-laravel/>

<h3>For</h3>

```
    @for
        <code>
    @endfor
```

<h3>Vazio</h3>

```php
    @empty
        <code>
    @endempty
```

<h3>Section</h3>

<h4>Passagem de variáveis como parâmetro</h4>

```php
    @yield('variable')

    @section('<variable>', '<string>')
```

<h4>Passagem de um trecho de código HTML como parâmetro</h4>

```php
    @yield('<string>')

    @section('<string>')

        <html-code-here>

    @endsection('<string>')
```

<h3 align="center">Realizar o link do diretório storage/app/public em public</h3>

```bash
    php artisan storage:link
```

<h2 align="center">GIT</h2>

```php
    story/102030-some-user-history-message
    
    hotfix/103031-some-hotfix-message

    bugfix/102032-some-bugfix-message
```

<h2 align="center">Upgrade Laravel App</h2>

* [ ] `CRIAR O DIRETÓRIO / NAMESPACE UTILS`

* [ ] `CRIAÇÃO DOS MODELS`

* [ ] `REFAZER AS MIGRAÇÕES E AS SEEDERS`

* [ ] `CRIAÇÃO DAS ROTAS E MIDDLEWARES`

* [ ] `CRIAÇÃO DAS VIEWS`

* [ ] `CONFIGURAÇÃO DOS ARQUIVOS NO DIRETÓRIO PUBLIC`

* [ ] `INSERÇÃO DO JAVASCRIPT EM RESOURCES / JS`

* [ ] `NPM INSTALL`

<h2 align="center">TODO - Version 1.0</h2>

👹 `Implementar a rotina de alteração de senha dentro do sistema.`

👹 `Implementar a rotina de restauração de senha através do e-mail cadastrado no usuário.`

👹 `Realizar o upload de imagens para o usuário, exibindo-a ao lado do nome.`

👹 `Realizar o cadastro de n imagens para um determinado produto.`

👹 `Na listagem, criar um carousel para exibição das imagens para um determinado produto.`

👹 `Desenvolver o cadastro dos locais de estoque.`

👹 `Desenvolver as regras para entrada / saída de itens dentro do sistema.`

👹 `Desenvolver a lógica de quantidade do produto por local de estoque.`

👹 `Realizar a exportação de XML e CSV para os módulos que possuam CSV.`

👹 `Criar o módulo Order, assim como o vínculo de n produtos para o mesmo.`

👹 `Criar o módulo forma de pagamento.`

👹 `Realizar o pagamento desse pedido.`

👹 `Criar os testes para todo o sistema.`

👹 `Documentar o sistema no estado atual.`

👹 `Lançar a primeira versão do sistema.`