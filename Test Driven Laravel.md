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

This lesson starts with how to upload the project to github.

In Goggle Chrome login to github. Click the New button.

- Call the Repository library
- Leave as a public
- click on Create repository

Follow the instructions to push an existing repository from teh command line.

```sh
git remote add origin https://github.com/Pen-y-Fan/library.git
git push -u origin master
```

```text
Enumerating objects: 141, done.
Counting objects: 100% (141/141), done.
Delta compression using up to 4 threads
Compressing objects: 100% (123/123), done.
Writing objects: 100% (141/141), 247.47 KiB | 2.29 MiB/s, done.
Total 141 (delta 24), reused 0 (delta 0)
remote: Resolving deltas: 100% (24/24), done.
To https://github.com/Pen-y-Fan/library.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

Before the lesson starts run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

....                                                                4 / 4 (100%)

Time: 372 ms, Memory: 20.00 MB

OK (4 tests, 8 assertions)
```

- All passing

Open **BookReservationTest.php**

- Remove the `$this->withoutExceptionHandling();`

Run all tests.

```text
...
OK (4 tests, 8 assertions)
...
```

- All green.

Next new test a book can be deleted

- add a new test method a_book_can_be_deleted
- Copy the update test code
- change the patch request to delete
- assert there is a count of 0 books
- add an interim check that there is a count of 1 book when the book is added
- without this additional check if no books are added the test will pass.

Run the test

```text
...
Failed asserting that actual size 1 matches expected size 0.

C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookReservationTest.php:78
...
```

- This hasn't highlighted the route doesn't exist, add `$this->withoutExceptionHandling();`

```php
/** @test */
public function a_book_can_be_deleted(): void
{
    $this->withoutExceptionHandling();
```

Run the test.

```text
...
Symfony\Component\HttpKernel\Exception\MethodNotAllowedHttpException: The DELETE method is not supported for this route. Supported methods: PATCH.
...
```

- This is the expected error, as the delete route doesn't exist.

Open **web.php**

- duplicate the patch route
- amend the copy to delete route and destroy method

```php
Route::post('/books', 'BooksController@store');
Route::patch('/books/{book}', 'BooksController@update');
Route::delete('/books/{book}', 'BooksController@destroy'); // Add
```

Run the test

```text
BadMethodCallException: Method App\Http\Controllers\BooksController::destroy does not exist.
```

- As expected the destroy method hasn't been created on the BooksController

Open **BooksController.php**

```php
public function destroy(Book $book)
{
    $book->delete();
}
```

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 281 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

- Passing.

Based on wishful programming, after a book is deleted the page should show the index.

- Add an additional assert that after the book is delete the site is redirected to /book (the index)

```php
// ...
$this->assertCount(0, Book::all());
$response->assertRedirect('/books'); // Add
// ...
```

```text
...
Response status code [200] is not a redirect status code.
Failed asserting that false is true.
...
```

- the test now fails, as there is no redirect to the books index.

Open **BooksController.php** delete method

- Add a redirect to /books (or used a named route)

```php
public function destroy(Book $book)
{
    $book->delete();

    return redirect('/books'); // Add
}
```

Run the test.

```text
...
OK (1 test, 4 assertions)
...
```

Refactor other tests.

- Once a book is updated the normal response to to redirect to the show view, the detail of the book.
- Add an assert that the response is redirected to `'books/' . $book->id`

```php
    $this->assertEquals('New Author', Book::first()->author);
    $response->assertRedirect('/books/' . $book->id); // Add
}
```

run that test

```text
...
Response status code [200] is not a redirect status code.
Failed asserting that false is true.
...
```

- As expected the test fails.

Open the **BookController.php** update method

- Add a return redirect to /books/ . \$book->id

```php
public function update(Book $book)
{
    $book->update($this->validateRequest());

    return redirect('/books/' . $book->id); // Add
}

```

```text
...
OK (1 test, 4 assertions)
...
```

Next refactor. After adding a book to a library:

- add a assertRedirect to /books/ \$book->id
- The \$book will need to be read from the database

```php
/** @test */
public function a_book_can_be_added_to_a_library(): void
{
    $response = $this->post('/books', [
        'title' => 'Cool Book Title',
        'author' => 'Victor',
    ]);

    $book = Book::first();

    $response->assertOk();
    $this->assertCount(1, Book::all());
    $response->assertRedirect('/books/' . $book->id);
}
```

Run this test

```text
...
Response status code [200] is not a redirect status code.
Failed asserting that false is true.
...
```

- as expected the test fails, the BooksController store method doesn't have a return redirect

Open **BooksController.php**

- copy the redirect fro the update method
- the create method will return the instance so add \$book =

```php
public function store()
{
    $book = Book::create($this->validateRequest()); // add $book =

    return redirect('/books/' . $book->id); // Copy from update method
}
```

Run the test

```text
...
Response status code [302] does not match expected 200 status code.
Failed asserting that false is true.

...
C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookReservationTest.php:22
...
```

- Line 22 is `$response->assertOk();`
- This doesn't need to be tested now the page is being redirected, so delete this line.

Run the test.

```text
...
OK (1 test, 3 assertions)
```

- Passes green.

Run all tests.

```text
...
OK (5 tests, 15 assertions)
```

Now all test a green the code can be refactored.

The author give a useful tip for redirecting instances of a model. Open **Book.php**

- create a helper public method called path
- which returns the normal math for that method, in this case '/books/ . \$this->id

```php
public function path()
{
    return '/books/' . $this->id;
}
```

Open **BooksController.php**

- Update the redirect to \$this->path()

```php
public function store()
{
    $book = Book::create($this->validateRequest());

    return redirect($book->path()); // Update
}

public function update(Book $book)
{
    $book->update($this->validateRequest());

    return redirect($book->path()); // Update
}
```

Rerun the test after each refactor.

```text
...
OK (5 tests, 15 assertions)
```

One more refactor, open **BookRefactorTest.php**

- in the a_book_can_be_deleted test remove the `$this->withoutExceptionHandling();`

Rerun all tests and still OK.

- rename the class BookManagementTest

Rerun all tests and still OK.

New test file

- called AuthorManagementTest

```sh
php artisan make:test AuthorManagementTest
```

Open **AuthorManagementTest.php**

- This will test the /author/ post route to add an author
- assert the author is added to the database
- refresh the database

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;

class AuthorManagementTest extends TestCase
{
    use RefreshDatabase;

    /** @test */
    public function an_author_can_be_created(): void
    {
        $this->withoutExceptionHandling();

        $this->post('/author', [
            'name' => 'Author Name',
            'dob' => '05/04/1988',
        ]);

        $this->assertCount(1, Author::all());
    }
}
```

Run the test

```text
...
Symfony\Component\HttpKernel\Exception\NotFoundHttpException: POST http://localhost/author
...
```

- As with Books, the post route doesn't exist.

Open **web.php**

- Add a post route for /author with store method

```php
// ...
Route::post('/author', 'AuthorsController@store');
```

Create the AuthorsController with a model

```sh
php artisan make:controller AuthorsController
```

```text
Controller created successfully.
```

Re-run the test

```text
...
BadMethodCallException: Method App\Http\Controllers\AuthorsController::store does not exist.
...
```

Open the **AuthorsController.php**

- Add a public method for store

```php
// ...
class AuthorsController extends Controller
{
    public function store()
    {
        // code
    }
}
```

Re-run the test

```text
...
Error: Class 'Tests\Feature\Author' not found
...
```

This is the model for Author

- run the php artisan command to make model Author with a migration

```sh
php artisan make:model Author -m
```

```text
Model created successfully.
Created Migration: 2019_06_25_110242_create_authors_table
```

Open the test **AuthorManagementTest.php**

- Import the model for Author
- Right Author in the line `click $this->assertCount(1, Author::all());` and import Class `use use App\Author;` will be added

Re-run the test

```text
...
Failed asserting that actual size 0 matches expected size 1.
...
```

This means the data wasn't added to the database.

Open the controller **AuthorsController.php**

- Create the record using **request**, this time use `request()->only(['name', 'dob',]);`

```php
// ...
use App\Author;

class AuthorsController extends Controller
{
    public function store()
    {
        Author::create(request()->only([
            'name', 'dob',
        ]));
    }
}
```

Re-run the test:

```text
...
Illuminate\Database\Eloquent\MassAssignmentException: Add [name] to fillable property to allow mass assignment on [App\Author].
...
```

As expected we have a mass assignment error, as fillable or guarded hasn't been set

- Open the Author model **Author.php**
- Add a `$guarded` array with 'id'

```php
class Author extends Model
{
    protected $guarded = ['id'];
}
```

Re-run the test

```text
Illuminate\Database\QueryException: SQLSTATE[HY000]: General error: 1 table authors has no column named name (SQL: insert into "authors" ("name", "dob", "updated_at", "created_at") values (Author Name, 05/04/1988, 2019-06-25 11:16:23, 2019-06-25 11:16:23))
...
Caused by
PDOException: SQLSTATE[HY000]: General error: 1 table authors has no column named name
...
```

The migration doesn't have any fields.

- Open **library\database\migrations\\...create_authors_table.php**
- Add the fields to the up() method

```php
// ...
public function up()
{
    Schema::create('authors', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->string('name');
        $table->timestamp('dob');
        $table->timestamps();
    });
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 409 ms, Memory: 18.00 MB

OK (1 test, 1 assertion)
```

Next is to refactor the test

- Check the dob is being stored as a carbon date format
- Open the test **AuthorManagementTest.php**
- Add a new assertion to check the dob is an instance of the Carbon class (Carbon is the class for dates)
- Refactor the test to return the Author data to an `$author` variable, as it is used in two assertions now.

```php
public function an_author_can_be_created(): void
{
    $this->withoutExceptionHandling();

    $this->post('/author', [
        'name' => 'Author Name',
        'dob' => '05/04/1988',
    ]);

    // Move the Author:all() from the first assertion to the $author variable
    $author = Author::all();

    $this->assertCount(1, $author);
    $this->assertInstanceOf(Carbon::class, $author->first()->dob);
}
```

Re-run the test

```text
...
Failed asserting that '05/04/1988' is an instance of class "Carbon\Carbon".
...
```

The test now fails, as the dob date isn't stored/retrieved as an instance of Carbon.

Open the Author model **Author.php**

- Create a protected \$dates property as an array, any fields specified in the array will be automatically based as carbon instances.

```php
class Author extends Model
{
    protected $guarded = ['id'];

    protected $dates = ['dob']; // Add
}
```

Re-run the tests

```text
...
InvalidArgumentException: Unexpected data found.
...
```

The date is not being specified within Laravel.

In the Author model

- Create a public function setDobAttribute
- Take the \$dob and update the attribute for dob to Carbon using its parse method

```php
// ...
use Carbon\Carbon; // Add / import

class Author extends Model
{
    protected $guarded = ['id'];

    protected $dates = ['dob'];

    // Create this method
    public function setDobAttribute($dob)
    {
        $this->attributes['dob'] = Carbon::parse($dob);
    }
}
```

Re-run the test

```text
...
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 561 ms, Memory: 18.00 MB

OK (1 test, 2 assertions)
```

Back in the test, the dob can be tested using carbon.

- Add a new assertion, with the data format set to yyyy/dd/mm and confirm Carbon can match that format

```php
// ...

    /** @test */
    public function an_author_can_be_created(): void
    {
        $this->withoutExceptionHandling();

        $this->post('/author', [
            'name' => 'Author Name',
            'dob' => '05/14/1988',  // Change the date format to an easier recognised mm/dd/yyyy
        ]);

        $author = Author::all();

        $this->assertCount(1, $author);
        $this->assertInstanceOf(Carbon::class, $author->first()->dob);
        $this->assertEquals('1988/14/05', $author->first()->dob->format('Y/d/m')); // Add this assertion
    }
```

Re-run the test

```text
...
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 358 ms, Memory: 18.00 MB

OK (1 test, 3 assertions)
...
```

This confirms the date is being saved as a carbon instance. It can be retrieved and re-formatted, in a different format, of a carbon instance.

## 03 25:11 Test Driven Laravel - e03 - Implementing a firstOrCreate Author Record With TDD

Before starting the lesson run all tests

```text
...
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.......                                                             7 / 7 (100%)

Time: 746 ms, Memory: 20.00 MB

OK (7 tests, 19 assertions)
...
```

They all pass.

- Always go from green state to green state.
- You never want to start a refactor in a red state.
- Any time we make a change to a test that will make it fail
- Then we change our code and we come back and rerun our tests
- If everything is right we-re back green.
- Do that over and over and over.

Currently, in the book reservation an author is a string.

- This should be checked against the database
- If the author doesn't exist one should be created
- If the author exists the author ID should be stored, for that author.

One way to select an author would be to type in an input box and the best match be available from the list.

Open **AuthorManagementTest.php**

- Remove \$this->withoutExceptionHandling();

```php
// ...
public function an_author_can_be_created(): void
    {
        $this->withoutExceptionHandling(); // Remove
        // ...
```

Run this test

```text
...
OK (1 test, 3 assertions)
...
```

The author is in the author management test, but it is also part of the book management

- The test could be in author or book management
- Recommendation is the endpoint (/books) being hit is in book, so the test should be part of the Book test.

Open **BookManagementTest.php** (this may still be named **BookReservationTest.php** - I missed the rename step earlier, rename as required)

- Add a new method a_new_author_is_automatically_added
- Copy the post array from the previous test
- Assign the book to the \$book variable
- Assign the Author to the \$author variable
- assert the Author is saved to the database (new database so will be 1)
- assert the author id matches the author_id
- import Author

```php
// ...
use App\Author;
// ...
/** @test */
public function a_new_author_is_automatically_added() :void
{
    $this->post('/books', [
        'title' => 'Cool Title',
        'author' => 'Victor',
    ]);

    $book = Book::first();
    $author = Author::first();

    $this->assertCount(1, Author::all());
    $this->assertEquals($author->id, $book->author_id); // Note: this originally book_id, but corrected to author_id later.
}
```

Run the test

```text
...
Failed asserting that actual size 0 matches expected size 1.
...
```

This is the count didn't match, the author isn't being saved to the author database.

- The test is a string with the author name, but the book table needs to save the author_id

Open **Author.php** (Note: this is moved to the Book model later)

- Create a helper function called set

```php
// ...
public function setAuthorAttribute($author)
{
    $this->attributes['author_id'] = Author::firstOrCreate([
        'name' => $author,
    ]);
}
// ...
```

Re-run the test

```text
...
Failed asserting that actual size 0 matches expected size 1.
...
```

Open the test **BookManagementTest.php**

- Flip the assertions, so the author id and book author id are compared first

```php
$this->assertEquals($author->id, $book->author_id); // Swap the order this assertion first
$this->assertCount(1, Author::all());
```

Re-run the test

```text
...
ErrorException: Trying to get property 'id' of non-object
...
```

We are trying to get an ID of something that doesn't exist

- The author didn't get created
- The date of birth is required, but we didn't see the error
- disable exception handling

```php
// ...
/** @test */
public function a_new_author_is_automatically_added() :void
{
    $this->withoutExceptionHandling();
// ...
```

Re-run the test

```text
...
ErrorException: Trying to get property 'id' of non-object
...
```

We are not seeing the actual error, other than the author isn't being created.

- When testing too high up a layer, use drop down a layer
- We are testing as a feature test
- For lower level testing, use unit tests
  - Interact with classes and objects directly

Open **tests\\Unit\\ExampleTest.php**, rename **AuthorTest.php**

- use RefreshDatabase
- create a test method called a_dob_is_nullable
- Create a new database entry for an author called John Doe
- Assert the data is in the database table

```php
<?php

namespace Tests\Unit;

use Tests\TestCase;
use Illuminate\Foundation\Testing\RefreshDatabase;
use App\Author;

class AuthorTest extends TestCase
{
    use RefreshDatabase;

    /** @test */
    public function a_dob_is_nullable() :void
    {
        Author::firstOrCreate([
            'name' => 'John Doe',
        ]);

        $this->assertCount(1, Author::all());
    }
}
```

Run this test

```text
...
PDOException: SQLSTATE[23000]: Integrity constraint violation: 19 NOT NULL constraint failed: authors.dob
...
```

We now have the actual error message, that wasn't being reached by the feature test.

In the unit test **AuthorTest.php**

- rename the test to only_name_is_required_to_create_an_author
- this is more descriptive on what is actually being tested

```php
/** @test */
public function only_name_is_required_to_create_an_author() :void
{
```

Open the create authors table **2019_06_25_110242_create_authors_table.php**

- update the dob filed so it is nullable

```php
public function up()
{
    Schema::create('authors', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->string('name');
        $table->timestamp('dob')->nullable(); // Update
        $table->timestamps();
    });
}
```

Re-run the unit test

```text
...
OK (1 test, 1 assertion)
...
```

Test now passes

- The author knew this was the error, but this wasn't being tested
- By writing a unit test TDD can be used to test the code from green to green
- Without a test, with the actual error, there is no reason to change the code

Return to the feature test **BookManagementTest.php**

Run the test

```text
...
ErrorException: Trying to get property 'id' of non-object
...
```

We know there is no author_id in book

- Drop down a level to unit test this

Create a unit test called BookTest

- use php artisan command

```sh
php artisan make:test BookTest --unit
# Test created successfully.
```

Open tests\\Unit\\**BookTest.php**

- Delete the example test
- Create a new test method called an_author_id_is_recorded
- Create a Book entry with the title and author_id
- Assert the data has been saved to the Book database table

```php
<?php

namespace Tests\Unit;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;
use App\Book;

class BookTest extends TestCase
{
    /** @test */
    public function an_author_id_is_recorded() :void
    {
        Book::create([
            'title' => 'Cool Title',
            'author_id' => 1,
        ]);
    }
}
```

Run the test

```text
...
PDOException: SQLSTATE[HY000]: General error: 1 no such table: books
...
```

The database need to be created before the test

- Add use RefreshDatabase;

```php
// ...
class BookTest extends TestCase
{
use RefreshDatabase; // Add

/** @test */
public function an_author_id_is_recorded() :void
// ...
```

Re-run the test

```text
...
PDOException: SQLSTATE[HY000]: General error: 1 table books has no column named author_id
...
```

The table need to be updated to add an author_id field

Open the books table.

- Add an author_id field with a type of unsignedBigInteger
- Do not delete author!

```php
public function up()
{
    Schema::create('books', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->string('title');
        $table->string('author');
        $table->unsignedBigInteger('author_id'); // Add
        $table->timestamps();
    });
}
```

Re-run the test

```text
...
PDOException: SQLSTATE[23000]: Integrity constraint violation: 19 NOT NULL constraint failed: books.author
...
```

Now there is a failing test

- Delete the author field

```php
public function up()
{
    Schema::create('books', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->string('title');
        $table->string('author');  // Delete this field
        $table->unsignedBigInteger('author_id');
        $table->timestamps();
    });
}
```

Re-run the test

```text
...
OK (1 test, 1 assertion)
...
```

Open the Book test **BookManagementTest.php**

- Run the a_new_author_is_automatically_added test

```text
...
PDOException: SQLSTATE[HY000]: General error: 1 table books has no column named author
...
```

We know that, as author has just been deleted

- The endpoint is being hit with an author string.
- check out the book controller

Open **BooksController.php**

- The request is being validated
- author is a required field
- Change author to author_id

```php
protected function validateRequest()
{
    return request()->validate([
        'title'  => 'required',
        'author_id' => 'required', // Update to author_id
    ]);
}
```

Open **Author.php** model

- Copy the setAuthorAttribute method to **Book.php**

In the **Book.php** model

- Rename the method name to setAuthorIdAttribute

Re-run the a_new_author_is_automatically_added test

```text
...
Illuminate\Validation\ValidationException: The given data was invalid.
...
```

Open the **BookManagementTest.php**

- The data being created is the author name as a string
- Change the field name to author_id

```php
// ...
$this->post('/books', [
    'title' => 'Cool Title',
    'author_id' => 'Victor',
]);
// ...
```

Re-run the test

```text
...
Failed asserting that '{"name":"Victor","updated_at":"2019-06-27 12:44:36","created_at":"2019-06-27 12:44:36","id":1}' matches expected 1.
C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookManagementTest.php:99
...
```

Open the test line 99 is the assertEquals check

- add die and dump for book->author_id

```php
$book = Book::first();
$author = Author::first();

dd($book->author_id); // Add a die and dump for author_id

$this->assertEquals($author->id, $book->author_id); // This line is failing
```

Re-run the test

```text
...
"{"name":"Victor","updated_at":"2019-06-27 12:49:03","created_at":"2019-06-27 12:49:03","id":1}"
...
```

The implementation must be incorrect.

Open **Book.php**

- Navigate to the setAuthorIdAttribute method

The way it is implemented, the record is being stored in the author_id field

- wrap the current record in parenthesis and pass the id

```php
public function setAuthorIdAttribute($author)
{
    $this->attributes['author_id'] = (Author::firstOrCreate([
        'name' => $author,
    ]))->id;
}
```

Re-run the test

```text
...
"1"
...
```

Open the test

- remove `dd($book->author_id);`

Re-run the test

```text
...
OK (1 test, 2 assertions)
...
```

The test now passes

- This is a big refactor
- The test was guiding the code
- the error guide what needs to be written

Run all tests

```text
...
...F.FEF.                                                           9 / 9 (100%)
...
ERRORS!
Tests: 9, Assertions: 13, Errors: 1, Failures: 3.
...
```

Now previous test are failing.

- Look at the test one at a time

Run a_book_can_be_added_to_a_library

```text
...
Failed asserting that actual size 0 matches expected size 1.

C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookManagementTest.php:23
...
```

The array being passed into the test need to be updated

- Currently author is a name

Before updating this refactor the way data is passed into the tests

- create a new private method called data from the array of data
- In the data method change the author to author_id

```php
public function a_book_can_be_added_to_a_library(): void
    {
        $response = $this->post('/books', $this->data()); // change the array to data method
// ...
// Add this private method, which returns the array data
private function data(): array
{
    return [
        'title' => 'Cool Book Title',
        'author_id' => 'Victor',
        ];
}
```

Re-run the test

```text
...
OK (1 test, 3 assertions)
...
```

That test now passes

Run all tests

```text
...
There were 2 failures:

1) Tests\Feature\BookManagementTest::an_author_is_required
...
ERRORS!
Tests: 9, Assertions: 15, Errors: 1, Failures: 2.
...
```

Next look at an_author_is_required

- the data is currently:

```php
$response = $this->post('/books', [
    'title' => 'Cool Book Title',
    'author' => '',
]);
```

This was to test an author can not be empty

- use the php function array_merge
- it take two arrays and returns the fields that match
- If there are duplicate keys the later key is used, which is useful to override the original data

```php
$response = $this->post('/books', array_merge($this->data(), ['author_id' => '']));
```

Run the test

```text
...
Session missing error: author
Failed asserting that false is true.
...
```

Update the test

- assert it is author_id

```php
/** @test */
public function an_author_is_required(): void
{
    $response = $this->post('/books', array_merge($this->data(), ['author_id' => '']));

    $response->assertSessionHasErrors('author_id');
}
```

Re-run the test

```text
...
OK (1 test, 2 assertions)
...
```

The test now passes

Re-run all tests

```text
...
......EF.                                                           9 / 9 (100%)

Time: 541 ms, Memory: 22.00 MB

...

There was 1 failure:

1) Tests\Feature\BookManagementTest::a_book_can_be_deleted
...
ERRORS!
Tests: 9, Assertions: 15, Errors: 1, Failures: 1.
...
```

Update the a_book_can_be_deleted test

- Change the old array to the new data method

```php
/** @test */
public function a_book_can_be_deleted(): void
{
    $this->post('/books', $this->data()); // Update

    $book = Book::first();
    $this->assertCount(1, Book::all());

    $response = $this->delete("/books/" . $book->id);

    $this->assertCount(0, Book::all());
    $response->assertRedirect('/books');
}
```

Re-run that test

```text
...
OK (1 test, 2 assertions)
...
```

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

......E..                                                           9 / 9 (100%)

Time: 521 ms, Memory: 22.00 MB

There was 1 error:

1) Tests\Feature\BookManagementTest::a_book_can_be_updated
ErrorException: Trying to get property 'id' of non-object

C:\laragon\www\YouTube\Test-Driven-Laravel\library\tests\Feature\BookManagementTest.php:53

ERRORS!
Tests: 9, Assertions: 18, Errors: 1.
```

Down to the last failing test.

- Update the array to use the data method

```php
$this->post('/books', $this->data());
```

Run the test

```text
...
--- Expected
+++ Actual
@@ @@
-'New Title'
+'Cool Book Title'
...
```

The data wasn't updated

- Update the path data to author_id

```php
$response = $this->patch("/books/" . $book->id, [
    'title' => 'New Title',
    'author_id' => 'New Author',
]);
```

Re-run the test

```text
...
Failed asserting that null matches expected 'New Author'.
...
```

Update the test

- assert the new author had an id of 1

```php
/** @test */
public function a_book_can_be_updated(): void
{
    $this->post('/books', $this->data());

    $book = Book::first();

    $response = $this->patch("/books/" . $book->id, [
        'title' => 'New Title',
        'author_id' => 'New Author',
    ]);

    $this->assertEquals('New Title', Book::first()->title);
    $this->assertEquals(1, Book::first()->author_id); // Update
    $response->assertRedirect('/books/' . $book->id);
}
```

Re-run the test

```text
...
Failed asserting that '2' matches expected 1.
...
```

When the fist book is created an author is created too, then the book is updated with a new author, another author is created

- Update the test to assert 2 matches the new author's ID

```php
$this->assertEquals(2, Book::first()->author_id); // Update
```

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.........                                                           9 / 9 (100%)

Time: 518 ms, Memory: 22.00 MB

OK (9 tests, 22 assertions)
```

All tests are back green.

- If a book is created an author is created, if the author doesn't exist.

## 04 28:43 Test Driven Laravel - e04 - Book Checkout & Book Checkin Flow With TDD

https://www.youtube.com/watch?v=CVKRBpBSXEw&list=PLpzy7FIRqpGAbkfdxo1MwOS9xjG3O3z1y&index=4
https://youtu.be/CVKRBpBSXEw?t=11
.

## 05 29:01 Test Driven Laravel - e05 - Book Checkout & Book Checkin Flow Feature Test With TDD - Part 2

https://www.youtube.com/watch?v=CVKRBpBSXEw&list=PLpzy7FIRqpGAbkfdxo1MwOS9xjG3O3z1y&index=5
.
