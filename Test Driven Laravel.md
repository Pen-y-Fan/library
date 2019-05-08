# Test Driven Laravel

<!-- cSpell: ignore Laravel beyondcode fideloper nesbot nunomaduro inflector lexer dragonmantank fzaninotto hamcrest filp webmozart erusev parsedown phpoption phpoption vlucas phpdotenv tijsverkoyen egulias swiftmailer swiftmailer paragonie ramsey opis monolog monolog flysystem jakub onderka nikic jakub onderka dnoegel psysh fzaninotto hamcrest filp webmozart phpdocumentor docblock phpunit theseer instantiator phpspec myclabs punycode libsodium PECL ircmaxell moontoast math UUIDs couchdb graylog gelf rollbar ruflin elastica eventable phpseclib webdav ziparchive spatie dropbox srmklive dbal guzzlehttp Mailgun nexmo pheanstalk predis wildbit libedit laragon editorconfig gitattributes gitignore styleci filesystems htaccess Csrf phpcs ruleset cmder Bergmann coderstape prettierrc -->

- [YouTube - Test Driven Laravel by coder's Tape](https://www.youtube.com/playlist?list=PLpzy7FIRqpGAbkfdxo1MwOS9xjG3O3z1y)
- [Github coderstape library](https://github.com/coderstape/library)

## Notes & disclaimer

- The purpose of these notes are to follow the above tutorial, making detailed notes of each step.
- They are not verbatim of the original video.
- Although the notes are detailed, it is possible they may not make sense out of context.
- The notes are not intended as a replacement the video series
  - Notes are more of a companion
  - They allow an easy reference search.
  - Allowing a particular video to be found and re-watched.
- During the notes two versions of PHPUnit are used:
  - 7.5.9 is installed with Laravel
  - 8.0.9 was previously installed globally, although this isn't the recommended way, it does allow PHPUnit to be run from any folder.
- Code snippets are often used to highlight the code changed, any code prior or post the code snipped is generally unchanged from previous notes, or to highlight only the output of interest. To signify a snippet of a larger code block, dots are normally used e.g.

```php
\\ ...
echo "Hello";
\\ ...
```

## 01. 28:26 Test Driven Laravel - e01 - Introduction, PHPUnit Setup & Books Test Part 1

The local library want software to manage the library. This will be a real world example. Including testing and source control (git & github).

- Books
- Due dates
- Meetings

Create a new project called library

```sh
laravel new library
```

```text
> laravel new library
Crafting application...
Loading composer repositories with package information
Installing dependencies (including require-dev) from lock file
Package operations: 76 installs, 0 updates, 0 removals
  - Installing doctrine/inflector (v1.3.0): Loading from cache
  - Installing doctrine/lexer (v1.0.1): Loading from cache
  - Installing dragonmantank/cron-expression (v2.3.0): Loading from cache
  - Installing erusev/parsedown (1.7.3): Loading from cache
  - Installing symfony/polyfill-ctype (v1.11.0): Loading from cache
  - Installing phpoption/phpoption (1.5.0): Loading from cache
  - Installing vlucas/phpdotenv (v3.3.3): Loading from cache
  - Installing symfony/css-selector (v4.2.8): Loading from cache
  - Installing tijsverkoyen/css-to-inline-styles (2.2.1): Loading from cache
  - Installing symfony/polyfill-php72 (v1.11.0): Loading from cache
  - Installing symfony/polyfill-mbstring (v1.11.0): Loading from cache
  - Installing symfony/var-dumper (v4.2.8): Loading from cache
  - Installing symfony/routing (v4.2.8): Loading from cache
  - Installing symfony/process (v4.2.8): Loading from cache
  - Installing symfony/http-foundation (v4.2.8): Loading from cache
  - Installing symfony/contracts (v1.0.2): Loading from cache
  - Installing symfony/event-dispatcher (v4.2.8): Loading from cache
....
Discovered Package: ←[beyondcode/laravel-dump-server←[
Discovered Package: ←[fideloper/proxy←[
Discovered Package: ←[laravel/tinker←[
Discovered Package: ←[nesbot/carbon←[
Discovered Package: ←[nunomaduro/collision←[
←Package manifest generated successfully.←[
Application ready! Build something amazing.
```

Change directory into the library folder and initialise git

```sh
cd library
git init
```

```text
Initialized empty Git repository in c:/laragon/www/YouTube/Test Driven Laravel/library/.git/
```

Laravel has allot of git ignore files built into the library.

To view the status of the library:

```sh
git status
```

```text
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .editorconfig
        .env.example
        .gitattributes
        .gitignore
        .styleci.yml
        app/
        artisan
        bootstrap/
        composer.json
        composer.lock
        config/
        database/
        package.json
        phpunit.xml
        public/
        resources/
        routes/
        server.php
        storage/
        tests/
        webpack.mix.js
        yarn.lock

nothing added to commit but untracked files present (use "git add" to track)
```

- Files are currently untracked.

To add all files:

```sh
git add .
```

To create the first commit (note: on Windows use double quotes)

```sh
git commit -m "initial commit"
```

```text
git commit -m "initial commit"
[master (root-commit) cd94563] initial commit
 88 files changed, 13362 insertions(+)
 create mode 100644 .editorconfig
 create mode 100644 .env.example
 create mode 100644 .gitattributes
 create mode 100644 .gitignore
 create mode 100644 .styleci.yml
 create mode 100644 app/Console/Kernel.php
 create mode 100644 app/Exceptions/Handler.php
 create mode 100644 app/Http/Controllers/Auth/ForgotPasswordController.php
 create mode 100644 app/Http/Controllers/Auth/LoginController.php
 create mode 100644 app/Http/Controllers/Auth/RegisterController.php
 create mode 100644 app/Http/Controllers/Auth/ResetPasswordController.php
 create mode 100644 app/Http/Controllers/Auth/VerificationController.php
 create mode 100644 app/Http/Controllers/Controller.php
 create mode 100644 app/Http/Kernel.php
 create mode 100644 app/Http/Middleware/Authenticate.php
 create mode 100644 app/Http/Middleware/CheckForMaintenanceMode.php
 create mode 100644 app/Http/Middleware/EncryptCookies.php
 create mode 100644 app/Http/Middleware/RedirectIfAuthenticated.php
 create mode 100644 app/Http/Middleware/TrimStrings.php
 create mode 100644 app/Http/Middleware/TrustProxies.php
 create mode 100644 app/Http/Middleware/VerifyCsrfToken.php
 create mode 100644 app/Providers/AppServiceProvider.php
 create mode 100644 app/Providers/AuthServiceProvider.php
 create mode 100644 app/Providers/BroadcastServiceProvider.php
 create mode 100644 app/Providers/EventServiceProvider.php
 create mode 100644 app/Providers/RouteServiceProvider.php
 create mode 100644 app/User.php
 create mode 100644 artisan
 create mode 100644 bootstrap/app.php
 create mode 100644 bootstrap/cache/.gitignore
 create mode 100644 composer.json
 create mode 100644 composer.lock
 create mode 100644 config/app.php
 create mode 100644 config/auth.php
 create mode 100644 config/broadcasting.php
 create mode 100644 config/cache.php
 create mode 100644 config/database.php
 create mode 100644 config/filesystems.php
 create mode 100644 config/hashing.php
 create mode 100644 config/logging.php
 create mode 100644 config/mail.php
 create mode 100644 config/queue.php
 create mode 100644 config/services.php
 create mode 100644 config/session.php
 create mode 100644 config/view.php
 create mode 100644 database/.gitignore
 create mode 100644 database/factories/UserFactory.php
 create mode 100644 database/migrations/2014_10_12_000000_create_users_table.php
 create mode 100644 database/migrations/2014_10_12_100000_create_password_resets_table.php
 create mode 100644 database/seeds/DatabaseSeeder.php
 create mode 100644 package.json
 create mode 100644 phpunit.xml
 create mode 100644 public/.htaccess
 create mode 100644 public/css/app.css
 create mode 100644 public/favicon.ico
 create mode 100644 public/index.php
 create mode 100644 public/js/app.js
 create mode 100644 public/robots.txt
 create mode 100644 resources/js/app.js
 create mode 100644 resources/js/bootstrap.js
 create mode 100644 resources/js/components/ExampleComponent.vue
 create mode 100644 resources/lang/en/auth.php
 create mode 100644 resources/lang/en/pagination.php
 create mode 100644 resources/lang/en/passwords.php
 create mode 100644 resources/lang/en/validation.php
 create mode 100644 resources/sass/_variables.scss
 create mode 100644 resources/sass/app.scss
 create mode 100644 resources/views/welcome.blade.php
 create mode 100644 routes/api.php
 create mode 100644 routes/channels.php
 create mode 100644 routes/console.php
 create mode 100644 routes/web.php
 create mode 100644 server.php
 create mode 100644 storage/app/.gitignore
 create mode 100644 storage/app/public/.gitignore
 create mode 100644 storage/framework/.gitignore
 create mode 100644 storage/framework/cache/.gitignore
 create mode 100644 storage/framework/cache/data/.gitignore
 create mode 100644 storage/framework/sessions/.gitignore
 create mode 100644 storage/framework/testing/.gitignore
 create mode 100644 storage/framework/views/.gitignore
 create mode 100644 storage/logs/.gitignore
 create mode 100644 tests/CreatesApplication.php
 create mode 100644 tests/Feature/ExampleTest.php
 create mode 100644 tests/TestCase.php
 create mode 100644 tests/Unit/ExampleTest.php
 create mode 100644 webpack.mix.js
 create mode 100644 yarn.lock
```

> "initial commit" is the common name for the fist commit

```sh
git status
```

```text
On branch master
nothing to commit, working tree clean
```

> This first lessons of this course will focus on the backend, with no fount end.

Open the editor (I use VS Code the tutor is using PHPStorm)

```sh
code .
```

In VS Code open **.env**

- Configure for sqlite

```text
DB_CONNECTION=sqlite
DB_HOST=127.0.0.1       }
DB_PORT=3306            }
DB_DATABASE=homestead   } remove
DB_USERNAME=homestead   }
DB_PASSWORD=secret      }
```

In the command line (I use cmder), create an empty database.sqlite file:

```sh
touch database\database.sqlite
```

Back in VS Code open **phpunit.xml** and setup for in memory sqlite database, add the lines:

- `<server name="BD_CONNECTION" value="sqlite"/>`
- `<server name="DB_DATABASE" value=":memory:"/>`

```xml
<php>
    <server name="APP_ENV" value="testing"/>
    <server name="BCRYPT_ROUNDS" value="4"/>
    <server name="CACHE_DRIVER" value="array"/>
    <server name="MAIL_DRIVER" value="array"/>
    <server name="QUEUE_CONNECTION" value="sync"/>
    <server name="SESSION_DRIVER" value="array"/>
    <server name="BD_CONNECTION" value="sqlite"/>
    <server name="DB_DATABASE" value=":memory:"/>
</php>
```

My setup: As I have the PHP CodeSniffer extension running, one thing I like to do before coding it to turn the error messages for comment blocks and camel case off. I found that coding errors were being ignored or missed due to the quantity of file and doc comment block errors. I have a file called **phpcs.ruleset.xml** which I locate in the route of the project, with my settings:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- PSR-2 but Doc Comment stuff removed -->
<ruleset name="Laravel no comments Standard">
  <description>The coding standard for Laravel with no comments</description>
  <rule ref="PSR2">
    <!-- Include rules related to Doc Comment I don't want -->
    <exclude name="PSR1.Methods.CamelCapsMethodName.NotCamelCaps"/>
    <exclude ref="Generic.Commenting.DocComment.ShortNotCapital" />
    <exclude ref="Generic.Commenting.DocComment.SpacingBeforeTags" />
    <exclude ref="Generic.Commenting.DocComment.TagValueIndent" />
    <exclude ref="Generic.Commenting.DocComment.NonParamGroup" />
    <exclude ref="PEAR.Commenting.FileComment.Missing" />
    <exclude ref="PEAR.Commenting.FileComment.MissingPackageTag" />
    <exclude ref="PEAR.Commenting.FileComment.PackageTagOrder" />
    <exclude ref="PEAR.Commenting.FileComment.MissingAuthorTag" />
    <exclude ref="PEAR.Commenting.FileComment.InvalidAuthors" />
    <exclude ref="PEAR.Commenting.FileComment.AuthorTagOrder" />
    <exclude ref="PEAR.Commenting.FileComment.MissingLicenseTag" />
    <exclude ref="PEAR.Commenting.FileComment.IncompleteLicense" />
    <exclude ref="PEAR.Commenting.FileComment.LicenseTagOrder" />
    <exclude ref="PEAR.Commenting.FileComment.MissingLinkTag" />
    <exclude ref="PEAR.Commenting.ClassComment.Missing" />
    <exclude ref="PEAR.Commenting.FunctionComment.Missing" />
    <exclude ref="PEAR.Commenting.FunctionComment.Missing" />
    <exclude ref="PEAR.Commenting.FunctionComment.MissingParamTag" />
    <exclude ref="PEAR.Commenting.FunctionComment.MissingParamName" />
    <exclude ref="PEAR.Commenting.FunctionComment.MissingParamComment" />
    <exclude ref="PEAR.Commenting.FunctionComment.MissingReturn" />
    <exclude ref="PEAR.Commenting.FunctionComment.SpacingAfter" />
  </rule>
</ruleset>
```

The integral thing about a library is books, they need ot be listed, added, edited etc. This will be the start of this project.

Open Feature\\**ExampleTest.php**, rename it **BookReservationTest.php**

- Open the file **BookReservationTest.php**
- Rename the class BookReservationTest
- Start writing the fist test called a_book_can_be_added_to_a_library
- given a POST endpoint is hit for a book with a title and author
- assert the book has been added to the database, it has a count of one.
- assert there was a successful response

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\RefreshDatabase;

class BookReservationTest extends TestCase
{
    /**
     * @test
     */
    public function a_book_can_be_added_to_a_library(): void
    {
        $response = $this->post('/books', [
            'title' => 'Book Book Title',
            'author' => 'Victor',
        ]);

        $response->assertOk();
        $this->assertCount(1, Book::all());
    }
}
```

Run the test and it fails:

```sh
vendor\bin\phpunit.bat --filter a_book_can_be_added_to_a_library
```

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

F                                                                   1 / 1 (100%)

Time: 967 ms, Memory: 16.00 MB

There was 1 failure:

1) Tests\Feature\BookReservationTest::a_book_can_be_added_to_a_library
Response status code [404] does not match expected 200 status code.
Failed asserting that false is true.

C:\laragon\www\YouTube\Test-Driven-Laravel\library\vendor\laravel\framework\src\Illuminate\Foundation\Testing\TestResponse.php:85
C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookReservationTest.php:20

FAILURES!
Tests: 1, Assertions: 1, Failures: 1.
```

- The 404 isn't a good test error, basically the page wasn't found, actually the route does not exist.
- Laravel is taking care of displaying the error as a http response.
- To see the real error add the line `$this->withoutExceptionHandling();`

```php
// ...
public function a_book_can_be_added_to_a_library(): void
{
    $this->withoutExceptionHandling();
    // ...
```

Re-run the test and a more useful error is displayed:

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

E                                                                   1 / 1 (100%)

Time: 1 second, Memory: 16.00 MB

There was 1 error:

1) Tests\Feature\BookReservationTest::a_book_can_be_added_to_a_library
Symfony\Component\HttpKernel\Exception\NotFoundHttpException: POST http://localhost/books

....

ERRORS!
Tests: 1, Assertions: 0, Errors: 1.
```

- `NotFoundHttpException: POST http://localhost/books` means there is a http exception, there is no POST route to /books

Open web routes file **web.php**

- Clear the existing route
- Create a post route to /books
- Based on wishful programming, enter a controller for BooksController store method

```php
<?php
// ...
Route::post('/books', 'BooksController@store');
```

Run the test

```text
...
1) Tests\Feature\BookReservationTest::a_book_can_be_added_to_a_library
ReflectionException: Class App\Http\Controllers\BooksController does not exist
...
```

- The answer is clear, the Class ... BooksController does not exist

Create the books controller

```sh
php artisan make:controller BooksController
```

```text
Controller created successfully.
```

Run the test again.

```text
...
BadMethodCallException: Method App\Http\Controllers\BooksController::store does not exist.
...
```

- Method ...\BooksController::store does not exist.
- The store method hasn't been created.

Open the **BooksController.php**

- Create an empty store method

```php
// ...
class BooksController extends Controller
{
    public function store()
    {
        // code
    }
}
```

Run the test again

```text
...
Error: Class 'Tests\Feature\Book' not found

... \tests\Feature\BookReservationTest.php:21
...
```

- It is looking for `Book` in the namespace 'Tests\Feature'
- line 21 of the test is `$this->assertCount(1, Book::all());`
- This is referring to the Model Book, which doesn't exist and the namespace hasn't been imported.

Create the model Book and a migration

```sh
php artisan make:model Book -m
```

```text
Model created successfully.
Created Migration: 2019_05_06_120614_create_books_table
```

Run the test give exactly the same error.

- the model has been created but the namespace hasn't been specified.
  - Either use `$this->assertCount(1, \App\Book::all());`
  - Or import the namespace, open tests\Feature\\**BookReservationTest.php**

```php
// ...
namespace Tests\Feature;

use App\Book; // Import the class.
use Tests\TestCase;
// ...
```

Run the test

```text
...
Illuminate\Database\QueryException: SQLSTATE[HY000]: General error: 1 no such table: books (SQL: select * from "books")
...
```

- Although there is a migration for book, there is no books table.
- Use the `RefreshDatabase` trait to migrate the database for every test, after every test the database will be taken down.

```php
// ...
class BookReservationTest extends TestCase
{
    use RefreshDatabase; // Add this trait
    /** @test */
    public function a_book_can_be_added_to_a_library(): void
// ...
```

Run the test

```text
...
Failed asserting that actual size 0 matches expected size 1.

C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookReservationTest.php:23
...
```

- This is line 23 of the test `$this->assertCount(1, Book::all());`
- The book hasn't been added to the database, if it had the database would have 1 book.

Open the **BookController.php**

- In the store method
  - create a record with a title and author from the request
  - validation will be added in the refactor stage.

```php
// ...
public function store()
{
    Book::create([
        'title' => request('title'),
        'author' => request('author')
    ]);
}
// ...
```

Run the test

```text
...
Symfony\Component\Debug\Exception\FatalThrowableError: Class 'App\Http\Controllers\Book' not found

C:\laragon\www\YouTube\Test-Driven-Laravel\library\app\Http\Controllers\BooksController.php:11
...
```

- Line 11 of BooksController is the `Book::create([`
- The Book Class doesn't exist in App\Http\Controllers
- Import the class App\Books

```php
// ...
namespace App\Http\Controllers;

use App\Book; // Import the class
use Illuminate\Http\Request;
// ...
```

Run the test

```text
...
Illuminate\Database\Eloquent\MassAssignmentException: Add [title] to fillable property to allow mass assignment on [App\Book].
...
```

- This is a Mass Assignment error, built in protection from Laravel.
- The fillable [or guarded] property hasn't been set to allow fields to be added to the database.

Open the model **Book.php**

- Add either the fillable properties or the guarded properties.
  - The tutor uses an empty array as an example: `protected $guarded = ['id'];`
  - I've added id to demonstrate a field can be protected.

```php
// ...
class Book extends Model
{
    protected $guarded = ['id'];
}
// ...
```

Run the test

```text
...
Illuminate\Database\QueryException: SQLSTATE[HY000]: General error: 1 table books has no column named title (SQL: insert into "books" ("title", "author", "updated_at", "created_at") values (Book Book Title, Victor, 2019-05-06 12:43:23, 2019-05-06 12:43:23))
...
Caused by
PDOException: SQLSTATE[HY000]: General error: 1 table books has no column named title
...
```

- books has no column named title
- a migration was created, when the model was created, but doesn't have any detail.

Open database\migrations\\**2019_05_06_120614_create_books_table.php**

- Add the fields title and author

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 362 ms, Memory: 18.00 MB

OK (1 test, 2 assertions)
```

- Test now passes.

Next do some validation testing. Open tests\Feature\\**BookReservationTest.php**

- Create a new test called a title is required
- Copy the start of the previous test
- Pass in a blank title
- Expect the response will have an error regarding title

```php
/** @test */
public function a_title_is_required() :void
{
    $this->withoutExceptionHandling();

    $response = $this->post('/books', [
        'title' => '',
        'author' => 'Victor',
    ]);

    $response->assertSessionHasErrors('title');
}
```

run the new test.

```sh
vendor\bin\phpunit --filter a_title_is_required
```

```text
...
Illuminate\Database\QueryException: SQLSTATE[23000]: Integrity constraint violation: 19 NOT NULL constraint failed: books.title (SQL: insert into "bo
oks" ("title", "author", "updated_at", "created_at") values (?, Victor, 2019-05-07 19:21:17, 2019-05-07 19:21:17))

...

Caused by
PDOException: SQLSTATE[23000]: Integrity constraint violation: 19 NOT NULL constraint failed: books.title
...
```

- There is no validation in place, the database is complaining.

Open **BooksController.php**

- perform a validate function on the request, in the store method

```php
public function store()
{
    $data = request()->validate([
        'title' => 'required',
    ]);
    Book::create($data);
}
```

Run the test

```text
...
Illuminate\Validation\ValidationException: The given data was invalid.
...
```

- In the test exception handling is being disabled, remove the line `$this->withoutExceptionHandling();`

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 336 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

The test now passes.

Run all tests

```text
...
1) Tests\Feature\BookReservationTest::a_book_can_be_added_to_a_library
Illuminate\Database\QueryException: SQLSTATE[23000]: Integrity constraint violation: 19 NOT NULL constraint failed: books.title (SQL: insert into "books" ("updated_at", "created_at") values (2019-05-07 19:34:01, 2019-05-07 19:34:01))
...
Caused by
PDOException: SQLSTATE[23000]: Integrity constraint violation: 19 NOT NULL constraint failed: books.title

...
```

- The first test now fails.
- Only title is being validated and then passed to the database using \$data

Open **BooksController.php**

- Add `'author' => ''` to the validate array.

```php
// ...
$data = request()->validate([
    'title'  => 'required',
    'author' => '',
]);
// ...
```

Run all tests and they pass

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

..                                                                  2 / 2 (100%)

Time: 298 ms, Memory: 20.00 MB

OK (2 tests, 4 assertions)
```

Create the next test

- an_author_is_required
- Copy the previous title test and change it to author
- The author field is blank this time.

```php
// ...
/** @test */
public function an_author_is_required(): void
{
    $response = $this->post('/books', [
        'title' => 'Cool Book Title',
        'author' => '',
    ]);

    $response->assertSessionHasErrors('author');
}
// ...
```

Run this test

```text
...
1) Tests\Feature\BookReservationTest::an_author_is_required
Session is missing expected key [errors].
Failed asserting that false is true.
...
```

- The assertion didn't have any errors.
- The author is being passed through without any validation

Open **BooksController.php**

- Update the validate for the author field to required

```php
$data = request()->validate([
    'title'  => 'required',
    'author' => 'required',
]);
```

Run the test

```text
...
OK (1 test, 2 assertions)
```

- It passes

Run all tests.

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

...                                                                 3 / 3 (100%)

Time: 327 ms, Memory: 20.00 MB

OK (3 tests, 6 assertions)
```

- All three pass.

New test a book can be updated

- Copy the post request to create a book from the a_book_can_be_added_to_a_library test
- Crete a patch request changing the title to new title
- assert the response from the patch matches the only book in the database (it is refreshed every time)
- Note: this was updated slightly from the order in the video

```php
/** @test */
public function a_book_can_be_updated(): void
{
    $this->post('/books', [
        'title' => 'Cool Title',
        'author' => 'Victor',
    ]);

    $book = Book::first();

    $response = $this->patch("/books/" . $book->id, [
        'title' => 'New Title',
        'author' => 'New Author',
    ]);

    $this->assertEquals('New Title', Book::first()->title);
    $this->assertEquals('New Author', Book::first()->author);
}
```

Run the test

```text
...
Failed asserting that two strings are equal.
--- Expected
+++ Actual
@@ @@
-'New Title'
+'Cool Book Title'
...
```

- add without exception handling to the test

```php
// ...
public function a_book_can_be_updated(): void
{
    $this->withoutExceptionHandling();
    // ...
```

Run the test

```text
...
Symfony\Component\HttpKernel\Exception\MethodNotAllowedHttpException: The PATCH method is not supported for this route. Supported methods: POST.
...
```

- the patch method hasn't been created in the route

Open **web.php**

- Add the patch verb.

```php
// ...
Route::post('/books', 'BooksController@store');
Route::patch('/books/{book}', 'BooksController@update');
```

```text
...
BadMethodCallException: Method App\Http\Controllers\BooksController::update does not exist.
...
```

- The update method doesn't exist on the BooksController

Open **BooksController.php**

- Create a public method for update

```php
public function update()
{
    // code
}
```

Run the test

```text
...
Failed asserting that two strings are equal.
--- Expected
+++ Actual
@@ @@
-'New Title'
+'Cool Title'
...
```

- The update isn't being added to the database.

Open **BookController.php**

- Add route model binding for Book
- Copy the validate from the store method
- Update the book

```php
public function update(Book $book)
{
    $data = request()->validate([
        'title'  => 'required',
        'author' => 'required',
    ]);
    $book->update($data);
}
```

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 395 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

- All green.

Run all tests.

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

....                                                                4 / 4 (100%)

Time: 419 ms, Memory: 20.00 MB

OK (4 tests, 8 assertions)
```

While green the code can be refactored.

Open **BookController.php**

- Take the validate array and turn it into a method called validateRequest
- Inline the validateRequest, there is no need to create the temporary variable \$data.

```php
<?php

namespace App\Http\Controllers;

use App\Book;
use Illuminate\Http\Request;

class BooksController extends Controller
{
    public function store()
    {
        Book::create($this->validateRequest());
    }

    public function update(Book $book)
    {
        $book->update($this->validateRequest());
    }

    protected function validateRequest()
    {
        return request()->validate([
            'title'  => 'required',
            'author' => 'required',
        ]);
    }
}
```

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

....                                                                4 / 4 (100%)

Time: 334 ms, Memory: 20.00 MB

OK (4 tests, 8 assertions)
```

- All green.

To wrap up the lesson

- do a git commit

```sh
git status
```

```text
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   phpunit.xml
        modified:   routes/web.php
        deleted:    tests/Feature/ExampleTest.php

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .prettierrc.json
        Test Driven Laravel.md
        app/Book.php
        app/Http/Controllers/BooksController.php
        database/migrations/2019_05_06_120614_create_books_table.php
        phpcs.ruleset.xml
        tests/Feature/BookReservationTest.php

no changes added to commit (use "git add" and/or "git commit -a")
```

In the video there is a php storm folder called .idea

Open **.gitignore**

- Add the .idea file
- I added .prettierrc.json and phpcs.ruleset.xml

```text
/node_modules
/public/hot
/public/storage
/storage/*.key
/vendor
.env
.phpunit.result.cache
Homestead.json
Homestead.yaml
npm-debug.log
yarn-error.log
/.idea
.prettierrc.json
phpcs.ruleset.xml
```

Run git status

```sh
git status
```

```text
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   .gitignore
        modified:   phpunit.xml
        modified:   routes/web.php
        deleted:    tests/Feature/ExampleTest.php

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        Test Driven Laravel.md
        app/Book.php
        app/Http/Controllers/BooksController.php
        database/migrations/2019_05_06_120614_create_books_table.php
        tests/Feature/BookReservationTest.php

no changes added to commit (use "git add" and/or "git commit -a")
```

- The settings files are no longer tracked.

Using VS Code, open the source control menu (CTRL SHIT G G) select the file(s) to commit by clicking on the + icon

- Choose gitignore and commit with the message e.g. update gitignore to exclude the .idea directory
- Choose Book.php, BookController.php and the migration, commit with a message adds the Book resource
- Choose phpunit.xlm with the comment adding testing database

## 02 26:32 Test Driven Laravel - e02 - Deleting a Record, Asserting Instance Of & Carbon Parse

.

## 03 25:11 Test Driven Laravel - e03 - Implementing a firstOrCreate Author Record With TDD

.
