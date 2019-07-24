# Test Driven Laravel

<!-- cSpell: ignore Laravel beyondcode fideloper nesbot nunomaduro inflector lexer dragonmantank fzaninotto hamcrest filp webmozart erusev parsedown phpoption phpoption vlucas phpdotenv tijsverkoyen egulias swiftmailer swiftmailer paragonie ramsey opis monolog monolog flysystem jakub onderka nikic jakub onderka dnoegel psysh fzaninotto hamcrest filp webmozart phpdocumentor docblock phpunit theseer instantiator phpspec myclabs punycode libsodium PECL ircmaxell moontoast math UUIDs couchdb graylog gelf rollbar ruflin elastica eventable phpseclib webdav ziparchive spatie dropbox srmklive dbal guzzlehttp Mailgun nexmo pheanstalk predis wildbit libedit laragon editorconfig gitattributes gitignore styleci filesystems htaccess Csrf phpcs ruleset cmder Bergmann coderstape prettierrc endsection tailwindcss enderror Bloggs -->

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

Run all tests

- Always start and end at green

```txt
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

..........                                                        10 / 10 (100%)

Time: 1.12 seconds, Memory: 22.00 MB

OK (10 tests, 23 assertions)
```

A library needs to check out a book

- Needs a book
- user
- Checkout time
- Return time

Create a test

- Book reservations test

```sh
php artisan make:test BookReservationsTest
```

```text
Test created successfully.
```

Open tests\Feature\\**BookReservationsTest.php**

- Clear the test case
- Create a new test method a_book_can_be_checked_out
- a book can call a checkout method, passing in a user
- or a user can checkout a book, passing in a book
- Another way it to grab the authenticated user, however this can limit the function e.g. i librarian can't check out a book for a user
- Avoid pivoting around the user object, as the user can do anything.
- The test will
  - Create a user object
  - Create a book object
  - Checkout a book, using a checkout method
  - Assert the database has 1 record
  - Assert the database user_id matches the data passed in
  - Assert the database book_id matches the data passed in
  - Assert the time stamp matches now

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;
use App\Book;
use App\User;

class BookReservationsTest extends TestCase
{
    use RefreshDatabase;

    /** @test */
    public function a_book_can_be_checked_out(): void
    {
        $book = factory(Book::class)->create();
        $user = factory(User::class)->create();

        $book->checkout($user);

        $this->assertCount(1, Reservation::all());
        $this->assertEquals($user->id, Reservation::first()->user_id);
        $this->assertEquals($book->id, Reservation::first()->book_id);
        $this->assertEquals(now(), Reservation::first()->checked_out_at);
    }
}
```

Checking th test that has been created, it isn't a feature test, as it isn't hitting an endpoint.

- Move the BookReservationTest into unit directory
  - tests\\**Unit**\\BookReservationsTest.php
- Rename the namespace Tests\Unit

```php
// ...
namespace Tests\Unit;
// ...
```

Run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
InvalidArgumentException: Unable to locate factory with name [default] [App\Book].
...
```

The Factory for Book hasn't been created

- Create a new factory for Book using artisan
- Use the -m option to pass in the Book model

```sh
php artisan make:factory BookFactory -m Book
```

```text
Factory created successfully.
```

Open database\factories\\**BookFactory.php**

- The factory has been created for the Book class.

Open database\migrations\\**2019_05_06_120614_create_books_table.php**

- Confirm the current fields:
  - title
  - author_id

Back in **BookFactory.php**

- Use faker to create some fake data
  - The title can be a sentence
  - The author_id
    - could be just 1
    - Or pass in a factory for Author (without creating the record)
- Remember to import Author class

```php
<?php

/* @var $factory \Illuminate\Database\Eloquent\Factory */

use App\Book;
use Faker\Generator as Faker;
use App\Author;

$factory->define(Book::class, function (Faker $faker) {
    return [
        'title' => $faker->sentence(),
        'author_id' => factory(Author::class),
    ];
});
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
InvalidArgumentException: Unable to locate factory with name [default] [App\Author].
...
```

The factory for Author hasn't been created

- Create a factory, using artisan, for an Author

```sh
php artisan make:factory AuthorFactory -m Author
```

```text
Factory created successfully.
```

Open the Author table, the see the required fields.

- name
- dob is nullable

Open database\factories\\**AuthorFactory.php**

- name can user faker name
- dob can use carbon, today's date minus 10 years

```php
<?php

/* @var $factory \Illuminate\Database\Eloquent\Factory */

use App\Author;
use Faker\Generator as Faker;

$factory->define(Author::class, function (Faker $faker) {
    return [
        'name' => $faker->name(),
        'dob' => now()->subYears(10),
    ];
});
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
BadMethodCallException: Call to undefined method App\Book::checkout()
...
```

The method checkout is undefined, as it hasn't been created, yet

- In the Book class
  - create a new public method called checkout

```php
// ...
public function checkout()
{
    // code
}
// ...
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
Error: Class 'Tests\Unit\Reservation' not found
...
```

The Reservation model \[class\] doesn't exist

- Create the model for Reservation
  - use the -m for the migration

```sh
php artisan make:model Reservation -m
```

```text
Created Migration: 2019_07_23_104204_create_reservations_table
```

Open the test tests\Unit\\**BookReservationsTest.php**

- Import the Reservation model

```php
// ...
use App\Reservation;
// ...
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
Failed asserting that actual size 0 matches expected size 1.
...
```

The data passed to checkout isn't being created in the database

Open app\\**Book.php**

- The checkout method needs:
  - user_id based in the \$user's id
  - checked_out_at which can be now()

```php
// ...
public function checkout($user)
{
    $this->reservations()->create([
        'user_id' => $user->id,
        'checked_out_at' => now(),
    ]);
}
// ...
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
BadMethodCallException: Call to undefined method App\Book::reservations()
...
```

The reservations method hasn't been created, yet, still in the Book model:

- Create a reservations public method
- return the relationship hasMany Reservations

```php
// ...
public function reservations()
{
    return $this->hasMany(Reservation::class);
}
// ...
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_checked_out
Illuminate\Database\Eloquent\MassAssignmentException: Add [user_id] to fillable property to allow mass assignment on [App\Reservation].
...
```

Mass assignment on Reservation. Open app\\**Reservation.php**

- Add a fillable or guarded array

```php
// ...
class Reservation extends Model
{
    protected $guarded = ['id'];
}
```

Re-run the test

```text
...
Caused by
PDOException: SQLSTATE[HY000]: General error: 1 table reservations has no column named user_id
...
```

The reservations table doesn't have a user_id field. Open the create reservations table database\migrations\\**2019_07_23_104204_create_reservations_table.php**

- Add user_id field to the up method

```php
public function up()
{
    Schema::create('reservations', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->unsignedBigInteger('user_id'); // Add
        $table->timestamps();
    });
}
```

Re-run the test

```text
...
Caused by
PDOException: SQLSTATE[HY000]: General error: 1 table reservations has no column named checked_out_at
...
```

The reservations database has no field called checked_out_at, open database\migrations \\**2019_07_23_104204_create_reservations_table.php**

- Add the checked_out_at field to the table, as a time stamp

```php
public function up()
{
    Schema::create('reservations', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->unsignedBigInteger('user_id');
        $table->timestamp('checked_out_at'); // Add
        $table->timestamps();
    });
}
```

Re-run the test

```text
...
Caused by
PDOException: SQLSTATE[HY000]: General error: 1 table reservations has no column named book_id
...
```

The reservations database has no field called book_id, open database\migrations \\**2019_07_23_104204_create_reservations_table.php**

- Add the book_id field to the table

```php
public function up()
{
    Schema::create('reservations', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->unsignedBigInteger('user_id');
        $table->unsignedBigInteger('book_id'); // Add
        $table->timestamp('checked_out_at');
        $table->timestamps();
    });
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 338 ms, Memory: 20.00 MB

OK (1 test, 4 assertions)
```

The test is now green

Next test is to return a book

Open tests\Unit\\**BookReservationsTest.php**

- copy the checkout test, as most of the code is the same
- After the book is checked out add a checked in method
- Update the book checked out test to book checked in

```php
/** @test */
public function a_book_can_be_returned(): void // New test name
{
    $book = factory(Book::class)->create();
    $user = factory(User::class)->create();

    $book->checkout($user);

    $book->checkin($user);  // Test a new method to checkin

    $this->assertCount(1, Reservation::all());
    $this->assertEquals($user->id, Reservation::first()->user_id);
    $this->assertEquals($book->id, Reservation::first()->book_id);
    $this->assertEquals(now(), Reservation::first()->checked_in_at); // Confirm the database check_in_at
}
```

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_returned
BadMethodCallException: Call to undefined method App\Book::checkin()
...
```

The checkin method doesn't exist. Open app\\**Book.php**

- Create a new public method called checkin

```php
// ...
public function checkin($user)
{
    // code
}
// ...
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_returned
null does not match expected type "object".
...
```

The line in the test is `$this->assertEquals(now(), Reservation::first()->checked_in_at);`

To confirm this is the problem:

- add a new assertNotNull test for \$this->assertNotNull(Reservation::first()->checked_in_at);

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_returned
Failed asserting that null is not null.
...
```

Open **Book.php**

- Update the checkin method
  - The reservation is a book that is checked out (the field is not null)
  - But not checked in (The checked in field is null)
- Update the reservation to make the book checked in.

```php
public function checkin($user)
{
    $reservation = $this->reservations()->where('user_id', $user->id)
        ->whereNotNull('checked_out_at')
        ->whereNull('checked_in_at')
        ->first();

    $reservation->update([
        'checked_in_at' => now(),
    ]);
}
```

Re-run the test

```text
...
1) Tests\Unit\BookReservationsTest::a_book_can_be_returned
Failed asserting that null is not null.
...
```

Currently checked_in_at filed doesn't exist in the table. Open create reservation table database\migrations\ **2019_07_23_104204_create_reservations_table.php**

- Add the checked_in_at field

```php
public function up()
{
    Schema::create('reservations', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->unsignedBigInteger('user_id');
        $table->unsignedBigInteger('book_id');
        $table->timestamp('checked_out_at');
        $table->timestamp('checked_in_at'); // Add
        $table->timestamps();
    });
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 301 ms, Memory: 20.00 MB

OK (1 test, 5 assertions)
```

The test now passes green.

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

............                                                      12 / 12 (100%)

Time: 1.64 seconds, Memory: 24.00 MB

OK (12 tests, 32 assertions)
```

The all pass green.

There are two edge cases highlighted by the tutor.

- If not checked out, then throw an exception
- A user can checkout a book twice (check it out, return it and check out again)

Open tests\Unit\ **BookReservationsTest.php**

- Create a new test

  - A user can checkout a book twice
  - Copy the code from a_book_can_be_returned
  - Update the test to check in the book, check it out and then back in
  - Assert record 2 in the database has the user_id, book_id, that is has been checked in is null, checked out is now
  - Checked the book back in again
  - Check record 2 has been updated, checked in is not null and it has a checked in date of now

```php
/** @test */
public function a_user_can_checkout_a_book_twice(): void
{
    $book = factory(Book::class)->create();
    $user = factory(User::class)->create();

    $book->checkout($user);
    $book->checkin($user);

    $book->checkout($user);

    $this->assertCount(2, Reservation::all());
    $this->assertEquals($user->id, Reservation::find(2)->user_id);
    $this->assertEquals($book->id, Reservation::find(2)->book_id);
    $this->assertNull(Reservation::find(2)->checked_in_at);
    $this->assertEquals(now(), Reservation::find(2)->checked_out_at);

    $book->checkin($user);

    $this->assertCount(2, Reservation::all());
    $this->assertEquals($user->id, Reservation::find(2)->user_id);
    $this->assertEquals($book->id, Reservation::find(2)->book_id);
    $this->assertNotNull(Reservation::find(2)->checked_in_at);
    $this->assertEquals(now(), Reservation::find(2)->checked_in_at);
}
```

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 655 ms, Memory: 20.00 MB

OK (1 test, 10 assertions)
```

All assertions from the test pass

Run all tests

```text
>vendor\bin\phpunit.bat
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.............                                                     13 / 13 (100%)

Time: 596 ms, Memory: 24.00 MB

OK (13 tests, 42 assertions)

```

They all pass.

Open tests\Unit\ **BookReservationsTest.php**.

- Create a new test if not checked out exception is thrown
- Copy some of the code from the previous test to create a book and user
- checkin the book (without it being checked out)
- expectException from the Exception class

```php
/** @test */
public function if_not_checked_out_exception_is_thrown(): void
{
    $this->expectException(\Exception::class);

    $book = factory(Book::class)->create();
    $user = factory(User::class)->create();

    $book->checkin($user);
}
```

Run the test

```text
...
1) Tests\Unit\BookReservationsTest::if_not_checked_out_exception_is_thrown
Failed asserting that exception of type "Error" matches expected exception "Exception". Message was: "Call to a member function update() on null" at
C:\laragon\www\YouTube\Test-Driven-Laravel\library\app\Book.php:31
...
```

Line 31 of Book.php is:

```php
$reservation->update([
    'checked_in_at' => now(),
]);
```

Basically \$reservation is null, as it wasn't found int eh database

- this can be confirmed by using `dd($reservation)`
- The quick code method is to add a check if \$reservation is null and throw an exception

```php
public function checkin($user)
{
    $reservation = $this->reservations()->where('user_id', $user->id)
        ->whereNotNull('checked_out_at')
        ->whereNull('checked_in_at')
        ->first();

    // Add this check:
    if (is_null($reservation)) {
        throw new \Exception();
    }

    $reservation->update([
        'checked_in_at' => now(),
    ]);
}

```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 297 ms, Memory: 20.00 MB

OK (1 test, 1 assertion)
```

It now passes.

Run all tests

```text
>vendor\bin\phpunit.bat
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

..............                                                    14 / 14 (100%)

Time: 846 ms, Memory: 24.00 MB

OK (14 tests, 43 assertions)
```

All tests pass.

Next lesson will create the end points to checkin and checkout books.

## 05 29:01 Test Driven Laravel - e05 - Book Checkout & Book Checkin Flow Feature Test With TDD - Part 2

<https://www.youtube.com/watch?v=CVKRBpBSXEw&list=PLpzy7FIRqpGAbkfdxo1MwOS9xjG3O3z1y&index=5>

First, run all the test

```text
C:\laragon\www\YouTube\Test-Driven-Laravel\library>vendor\bin\phpunit.bat
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

..............                                                    14 / 14 (100%)

Time: 674 ms, Memory: 12.00 MB

OK (14 tests, 43 assertions)
```

All tests pass green.

This lesson will focus on the endpoint for the Book reservation.

First make a test for BookCheckoutTest

```sh
php artisan make:test BookCheckoutTest
```

```text
Test created successfully.
```

This will be a feature test. Open tests\Feature\ **BookCheckoutTest.php**

- Remove the example test
- Start a fresh test
  - Create a book
  - Create a user and post to /checkout/ with the book id
  - Copy the assertions from the tests\Unit\ **BookReservationsTest.php** a_book_can_be_checked_out method
  - Import Book, User and Reservation

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;
use App\Book;
use App\User;
use App\Reservation;

class BookCheckoutTest extends TestCase
{
    /** @test */
    public function a_book_can_be_checked_out_by_a_signed_in_user(): void
    {
        $book = factory(Book::class)->create();
        $user = Factory(User::class)->create();

        $this->actingAs($user)
            ->post('/checkout/' . $book->id);

        $this->assertCount(1, Reservation::all());
        $this->assertEquals($user->id, Reservation::first()->user_id);
        $this->assertEquals($book->id, Reservation::first()->book_id);
        $this->assertEquals(now(), Reservation::first()->checked_out_at);
    }
}
```

Run the test

```text
...
Caused by
PDOException: SQLSTATE[HY000]: General error: 1 no such table: authors
...
```

The database hasn't been created

- Add use RefreshDatabase

```php
// ...
use RefreshDatabase;
// ...
```

Re-run the test

```text
...
Failed asserting that actual size 0 matches expected size 1.
...
```

The data hasn't been added to the database, but the actual error is being hidden

- Add withoutExceptionHandling

```php
$this->withoutExceptionHandling();
```

Re-run the test

```text
...
Symfony\Component\HttpKernel\Exception\NotFoundHttpException: POST http://localhost/checkout/1
...
```

There is no route for checkout

- Open routes\ **web.php**
- Create a route for post to /checkout/ and hit the CheckoutBookController store method

```php
// ...
Route::post('/checkout/{book}', 'CheckoutBookController@store');
// ...
```

Re-run the test

```text
...
ReflectionException: Class App\Http\Controllers\CheckoutBookController does not exist
...
```

CheckoutBookController hasn't been created

- Create the controller

```sh
php artisan make:controller CheckoutBookController
```

```text
Controller created successfully.
```

Re-run the test

```text
...
BadMethodCallException: Method App\Http\Controllers\CheckoutBookController::store does not exist.
...
```

The store method hasn't been created

- Open app\Http\Controllers\ **CheckoutBookController.php**
- Add a store method

```php
class CheckoutBookController extends Controller
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
Failed asserting that actual size 0 matches expected size 1.
...
```

The book hasn't been added to the database

- Use the checkout method from the test
- The book will passed in as a variable, this can be type hinted to the Book class
- Import the Book class
- The user will be the authenticated user

```php
public function store(Book $book)
{
    $book->checkout(auth()->user());
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 688 ms, Memory: 10.00 MB

OK (1 test, 4 assertions)
```

the test is now green.

The next test is only signed in users can checkout a book.

- Copy the a_book_can_be_checked_out_by_a_signed_in_user test
- rename only_signed_in_users_can_checkout_a_book
- Remove the line Exception handling from both tests
- Remove the acting as authenticated user
- Add assertRedirect to the login page
- Assert the database is 0

```php
//...
public function a_book_can_be_checked_out_by_a_signed_in_user(): void
{
    $this->withoutExceptionHandling(); // Delete
    //...

/** @test */
public function only_signed_in_users_can_checkout_a_book(): void
{
    $book = factory(Book::class)->create();

    $this->post('/checkout/' . $book->id)
        ->assertRedirect('/login');

    $this->assertCount(0, Reservation::all());
}
// ...
```

Run the test

```text
...
Response status code [500] is not a redirect status code.
...
```

Add without exception handling to the test to find the error.

```php
// ...
public function only_signed_in_users_can_checkout_a_book(): void
{
    $this->withoutExceptionHandling();
// ...
```

Re-run the test

```text
...
ErrorException: Trying to get property 'id' of non-object

... \library\app\Book.php:19
...
```

Open Book.php

- `'user_id' => $user->id,`
- User is actually null
- Add a constructor the to CheckoutBookController
- Use the Laravel middleware('auth')

```php
// ....
class CheckoutBookController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth');
    }

    public function store(Book $book)
// ...
```

Re-run the test

```text
...
InvalidArgumentException: Route [login] not defined.
...
```

Turn off exception handling and re-run the test again.

```text
...
Response status code [500] is not a redirect status code.
...
```

To check the routes

- Run the artisan command route:list

```sh
php artisan route:list
```

| Domain | Method     | URI             | Name | Action                                            | Middleware   |
| ------ | ---------- | --------------- | ---- | ------------------------------------------------- | ------------ |
|        | GET\| HEAD | api/user        |      | Closure                                           | api,auth:api |
|        | POST       | author          |      | App\Http\Controllers\AuthorsController@store      | web          |
|        | POST       | books           |      | App\Http\Controllers\BooksController@store        | web          |
|        | PATCH      | books/{book}    |      | App\Http\Controllers\BooksController@update       | web          |
|        | DELETE     | books/{book}    |      | App\Http\Controllers\BooksController@destroy      | web          |
|        | POST       | checkout/{book} |      | App\Http\Controllers\CheckoutBookController@store | web,auth     |

There is no route for login

- run the artisan command make:auth

```sh
php artisan make:auth
```

```text
Authentication scaffolding generated successfully.
```

Run the artisan route list again

```sh
php artisan route:list
```

| Domain | Method    | URI                    | Name             | Action                                                                 | Middleware   |
| ------ | --------- | ---------------------- | ---------------- | ---------------------------------------------------------------------- | ------------ |
|        | GET\|HEAD | api/user               |                  | Closure                                                                | api,auth:api |
|        | POST      | author                 |                  | App\Http\Controllers\AuthorsController@store                           | web          |
|        |
|        | POST      | books                  |                  | App\Http\Controllers\BooksController@store                             | web          |
|        |
|        | PATCH     | books/{book}           |                  | App\Http\Controllers\BooksController@update                            | web          |
|        |
|        | DELETE    | books/{book}           |                  | App\Http\Controllers\BooksController@destroy                           | web          |
|        |
|        | POST      | checkout/{book}        |                  | App\Http\Controllers\CheckoutBookController@store                      | web,auth     |
|        |
|        | GET\|HEAD | home                   | home             | App\Http\Controllers\HomeController@index                              | web,auth     |
|        |
|        | GET\|HEAD | login                  | login            | App\Http\Controllers\Auth\LoginController@showLoginForm                | web,guest    |
|        |
|        | POST      | login                  |                  | App\Http\Controllers\Auth\LoginController@login                        | web,guest    |
|        |
|        | POST      | logout                 | logout           | App\Http\Controllers\Auth\LoginController@logout                       | web          |
|        |
|        | POST      | password/email         | password.email   | App\Http\Controllers\Auth\ForgotPasswordController@sendResetLinkEmail  | web,guest    |
|        |
|        | GET\|HEAD | password/reset         | password.request | App\Http\Controllers\Auth\ForgotPasswordController@showLinkRequestForm | web,guest    |
|        |
|        | POST      | password/reset         | password.update  | App\Http\Controllers\Auth\ResetPasswordController@reset                | web,guest    |
|        |
|        | GET\|HEAD | password/reset/{token} | password.reset   | App\Http\Controllers\Auth\ResetPasswordController@showResetForm        | web,guest    |
|        |
|        | GET\|HEAD | register               | register         | App\Http\Controllers\Auth\RegisterController@showRegistrationForm      | web,guest    |
|        |
|        | POST      | register               |                  | App\Http\Controllers\Auth\RegisterController@register                  | web,guest    |
|        |

All the routes for authenticating users are created.

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 663 ms, Memory: 10.00 MB

OK (1 test, 3 assertions)
```

The test is now green.

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

................                                                  16 / 16 (100%)

Time: 709 ms, Memory: 14.00 MB

OK (16 tests, 50 assertions)
```

They all pass

Next test a book needs to exist before it can be checked out

- Copy the a_book_can_be_checked_out_by_a_signed_in_user test
- rename it only_real_books_can_be_checked_out
- remove the line to create a book
- post to checkout with a made up book number (123)
- assert a status code of 404 (not found)

```php
// ...
/** @test */
public function only_real_books_can_be_checked_out(): void
{
    $user = Factory(User::class)->create();

    $this->actingAs($user)
        ->post('/checkout/' . 123) // Book 123 is a made up number
        ->assertStatus(404);

    $this->assertCount(0, Reservation::all());
// ...
}
```

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 610 ms, Memory: 10.00 MB

OK (1 test, 2 assertions)
```

Next test, based on tests\Unit\ **BookReservationsTest.php**, a_book_can_be_returned

- Copy the test a_book_can_be_checked_out_by_a_signed_in_user
- Rename it a_book_can_be_checked_in_by_a_signed_in_user
- Add a new checkin endpoint, passing in the book id
- Add an additional assertion for checked in at

```php
// ...
/** @test */
public function a_book_can_be_checked_in_by_a_signed_in_user(): void
{
    $book = factory(Book::class)->create();
    $user = Factory(User::class)->create();
    $this->actingAs($user)
        ->post('/checkout/' . $book->id);

    $this->actingAs($user)
        ->post('/checkin/' . $book->id);  // Add

    $this->assertCount(1, Reservation::all());
    $this->assertEquals($user->id, Reservation::first()->user_id);
    $this->assertEquals($book->id, Reservation::first()->book_id);
    $this->assertEquals(now(), Reservation::first()->checked_out_at);
    $this->assertEquals(now(), Reservation::first()->checked_in_at); // Add
}
// ...
```

Run the test

```text
...
null does not match expected type "object".

... tests\Feature\BookCheckoutTest.php:71
...
```

Line 71 is the assertion for checked_in_at

- Disable exception handling

```php
$this->withoutExceptionHandling();
```

Re-run the test

```text
...
Symfony\Component\HttpKernel\Exception\NotFoundHttpException: POST http://localhost/checkin/1
...
```

There is no checkin route.

- Create the route in routes\ **web.php**
- For the /checkin/ route with book and hit the CheckinBookController's store method

```php
// ...
Route::post('/checkin/{book}', 'CheckinBookController@store');
// ...

```

Re-run the test

```text
...
ReflectionException: Class App\Http\Controllers\CheckinBookController does not exist
...
```

CheckinBookController hasn't been created, yet.

- Run the php artisan command to make controller for CheckinBookController

```sh
php artisan make:controller CheckinBookController
```

```text
Controller created successfully.
```

Re-run the test

```text
...
BadMethodCallException: Method App\Http\Controllers\CheckinBookController::store does not exist.
...
```

The store method hasn't been created, yet.

- Open CheckinBookController
- Create a new method for store

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Book;

class CheckinBookController extends Controller
{
    public function store(Book $book)
    {
        // code
    }
}
```

Re-run the test

```text
...
null does not match expected type "object".
...
```

Update the store method

- Based on the unit test `$book->checkin($user);`
- As with checkout, amend it for `auth()->user();`
- Type hint Book and import the class

```php
// ...
use App\Book;
// ...
public function store(Book $book)
{
    $book->checkin(auth()->user());
}
// ...
```

Re-run the test.

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 743 ms, Memory: 20.00 MB

OK (1 test, 5 assertions)
```

Next test

- Only signed in users can checkin a book
- Copy the checkout version of the same test.

```php
/** @test */
public function a_book_can_be_checked_in_by_a_signed_in_user(): void
{
    $book = factory(Book::class)->create();
    $this->post('/checkout/' . $book->id)
        ->assertRedirect('/login');

    $this->post('/checkin/' . $book->id)
        ->assertRedirect('/login');

    $this->assertCount(0, Reservation::all());
    $this->assertEquals($user->id, Reservation::first()->user_id);
    $this->assertEquals($book->id, Reservation::first()->book_id);
    $this->assertEquals(now(), Reservation::first()->checked_out_at);
    $this->assertEquals(now(), Reservation::first()->checked_in_at);
}
```

Run the test

```text
...
Response status code [500] is not a redirect status code.
...
```

To find the real error

- Add without exception handling

```php
// ...
$this->withoutExceptionHandling();
// ...
```

Re-run the test

```text
...
Illuminate\Auth\AuthenticationException: Unauthenticated.
...
```

For the book the be created the user needs to be authenticated

- Alter the test so the checkout is acting as a user

```php
// ...
$this->actingAs($user)
    ->post('/checkout/' . $book->id);
// ...
```

Re-run the test

```text
...
Response status code [200] is not a redirect status code.
...
```

As with the CheckoutBookController

- Add a construct
  - use the middleware auth

```php
public function __construct()
{
    $this->middleware('auth');
}
```

Re-run the test

```text
...
Response status code [200] is not a redirect status code.
...
```

This is unexpected, as the logout isn't actingAs the user. When a user is logged in Laravel keeps the user login.

- Add a logout line after the book has been checked out

```php
// ...
Auth::logout();
// ...
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 332 ms, Memory: 22.00 MB

OK (1 test, 3 assertions)
```

To check the checked_in_at is Null

- Add an AssertNull for checked_in_at

```php
// ...
$this->assertNull(Reservation::first()->checked_in_at);
// ...
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 332 ms, Memory: 22.00 MB

OK (1 test, 4 assertions)
```

The test passes.

The next test is only real books can be checked in

```php
/** @test */
public function only_real_books_can_be_checked_in(): void
{
    $user = Factory(User::class)->create();

    $this->actingAs($user)
        ->post('/checkin/' . 123)
        ->assertStatus(404);

    $this->assertCount(0, Reservation::all());
}
```

The tutor doesn't think we need to test this, as the book couldn't have been created anyway.

Run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 365 ms, Memory: 22.00 MB

OK (1 test, 2 assertions)
```

Run the test class

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

......                                                              6 / 6 (100%)

Time: 609 ms, Memory: 22.00 MB

OK (6 tests, 20 assertions)
```

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

....................                                              20 / 20 (100%)

Time: 787 ms, Memory: 26.00 MB

OK (20 tests, 63 assertions)
```

Next test, based on the unit test if_not_checked_out_exception_is_thrown

- Create a new test a_404_is_thrown_if_a_book_is_not_checked_out_first
- Copy the test code from only_signed_in_users_can_checkin_a_book this will be the basis of the test
- Create a book
- Create a user
- Remove the line to checkout
- Acting as the user checkin the book

```php
/** @test */
public function a_404_is_thrown_if_a_book_is_not_checked_out_first(): void
{
    $book = factory(Book::class)->create();
    $user = factory(User::class)->create();

    $this->actingAs($user)
        ->post('/checkin/' . $book->id)
        ->assertStatus(404);

    $this->assertCount(0, Reservation::all());
}
```

Run the test

```text
...
Expected status code 404 but received 500.
...
```

As before add

- withoutExceptionHandling

```php
// ...
$this->withoutExceptionHandling();
// ...
```

Re-run the test

```text
...
Exception:

...\library\app\Book.php:32
...
```

Book line 32 is:

```php
throw new \Exception();
```

Open the **CheckinBookController**, in the store method

- add a try catch block
- try to checkin the book
- catch the exception and return a response of 404

```php
public function store(Book $book)
{
    try {
        $book->checkin(auth()->user());
    } catch (\Exception $e) {
        return response([], 404);
    }
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 301 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

The test now passes

- Clear the exception handling

Run the test class

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.......                                                             7 / 7 (100%)

Time: 535 ms, Memory: 22.00 MB

OK (7 tests, 22 assertions)
```

Run all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.....................                                             21 / 21 (100%)

Time: 735 ms, Memory: 26.00 MB

OK (21 tests, 65 assertions)
```

## 06 28:36 Test Driven Laravel - e06 - Testing Validation, Importing Vue.js & Tailwind CSS

First start by running all tests

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.....................                                             21 / 21 (100%)

Time: 735 ms, Memory: 26.00 MB

OK (21 tests, 65 assertions).
```

The AuthorManagementTest has a test for the endpoint of /author, however the same test in the BookManagementTest has an endpoint of Books, to keep things consistent:

- open tests\Feature\ **AuthorManagementTest.php**
- amend the endpoint from /author to /authors

```php
// ...
/** @test */
public function an_author_can_be_created(): void
{
    // Was: /author
    $this->post('/authors', [
        'name' => 'Author Name',
        'dob' => '05/14/1988',
    ]);
// ...
```

Run the test

```text
...
Failed asserting that actual size 0 matches expected size 1.
...
```

Update the route

- Open routes\ **web.php**
- Update author to /authors (keeps the routes consistent too)

```php
Route::post('/authors', 'AuthorsController@store');
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 464 ms, Memory: 18.00 MB

OK (1 test, 3 assertions)
```

Back in **AuthorManagementTest.php**

Create a data method, same principle as was created data in the BookManagementTest and use array_merge to override parts of the data

```php
/** @test */
public function an_author_can_be_created(): void
{
    $this->post('/authors', $this->data()); // Change the array with data to private data method
    // ....
}

private function data()
{
    return [
        'name' => 'Author Name',
        'dob' => '05/14/1988',
    ];
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 349 ms, Memory: 18.00 MB

OK (1 test, 3 assertions)
```

Still in the **AuthorManagementTest.php**

- Create a new test a_name_is_required
- Copy the post with data line from the previous test and amend the data using array_merge
- Override the name filed to an empty string
- assert the session has errors on name

```php
/** @test */
public function a_name_is_required(): void
{
    $response = $this->post('/authors', array_merge($this->data(), ['name' => '']));

    $response->assertSessionHasErrors('name');
}
```

Run the test

```text
...
Session is missing expected key [errors].
Failed asserting that false is true.
...
```

The AuthorsController doesn't currently validate any data.

- Open app\Http\Controllers\ **AuthorsController.php**
- Add the fields to be validated
- Create the record based on the validated data

```php
public function store()
{
    $data = request()->validate([
        'name' => 'required',
        'dob' => '',
    ]);

    Author::create($data);
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 372 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

The test now passes.

Next test a dob is required

- copy the a_name_is_required test
- rename is a_dob_is_required test
- change the override to dob

```php
/** @test */
public function a_dob_is_required(): void
{
    $response = $this->post('/authors', array_merge($this->data(), ['dob' => '']));

    $response->assertSessionHasErrors('dob');
}
```

Run the test

```text
...
Session is missing expected key [errors].
...
```

Open **AuthorsController.php**

- Update the dob to required

```php
$data = request()->validate([
    'name' => 'required',
    'dob' => 'required', // Update
]);
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 501 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

It now passes.

In the **BooksController**

- There is a validateRequest protected method, which can be re-used in the class

Open the **AuthorsController.php**

- Create a validateRequest protected method based on the current request()->validate... requirements ...
- Inline the Author::create with the validateRequest

```php
class AuthorsController extends Controller
{
    public function store()
    {
        Author::create($this->validateRequest());
    }

    protected function validateRequest()
    {
        return request()->validate([
            'name' => 'required',
            'dob' => 'required',
        ]);
    }
}
```

Re-run the test

```text
PHPUnit 7.5.9 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 280 ms, Memory: 20.00 MB

OK (1 test, 2 assertions)
```

Still green

Next a look at some front end website work with Vue.js and Tailwind CSS.

Laravel ships with the preset of vue and bootstrap.

- run the artisan preset none to remove both vue and bootstrap

```sh
php artisan preset none
```

```text
Frontend scaffolding removed successfully.
```

App.scss, app.js and bootstrap.js have been emptied or the minimum required is left.

- run the artisan preset vue command to bring in vue

```sh
php artisan preset vue
```

```text
Vue scaffolding installed successfully.
Please run "npm install && npm run dev" to compile your fresh scaffolding.
```

**app.js** now has the line `window.Vue = require('vue');`

Run npm install

```sh
npm install
```

```text
...
added 1001 packages from 477 contributors and audited 17139 packages in 97.134s
found 0 vulnerabilities
```

Open <https://tailwindcss.com/docs/installation/>

Follow the documentation

```sh
npm install tailwindcss -save-dev
```

```text
added 15 packages from 52 contributors and audited 17258 packages in 16.721s
found 0 vulnerabilities
```

Open **app.scss**

Paste in (from the website)

```scss
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Continuing from the install doc

- Create a config file (note: np**x** not np**m**)

```sh
npx tailwind init
```

```text
tailwindcss 1.0.5

✅ Created Tailwind config file: tailwind.config.js
```

- Scroll down to Laravel Mix section, Laravel uses sass.
- Copy the options({...})

Open webpack.mix.js

```js
const mix = require("laravel-mix");
const tailwindcss = require("tailwindcss");
// ...
mix
 .js("resources/js/app.js", "public/js")
 .sass("resources/sass/app.scss", "public/css")
 .options({
  processCssUrls: false,
  postCss: [tailwindcss("./tailwind.config.js")]
 });
```

Run npm run dev

```sh
npm run dev
```

This takes a few minutes to run.

```text
 DONE  Compiled successfully in 9218ms

       Asset     Size   Chunks             Chunk Names
/css/app.css  481 KiB  /js/app  [emitted]  /js/app
  /js/app.js  922 KiB  /js/app  [emitted]  /js/app
```

Open resources\views\layouts\ **app.blade.php**

- Comment out all of the navbar (it contains bootstrap classes)
- Remove the fonts
- Change the app.name to Library

Open app\Http\Controllers\ **AuthorsController.php**

- Add a new create method
- return a view 'authors.create'

```php
public function create()
{
    return view('authors.create');
}
```

Create a new file resources\views\authors\ **create.blade.php**

```php
@extends('layouts.app')

@section('content')
    <div class="bg-grey-300 h-screen">
        abcde
    </div>
@endsection
```

Open routes\ **web.php**

```php
Route::get('/authors/create', 'AuthorsController@create');
```

Open the browser and navigate to the project <http://youtube.library.test/authors/create>

- If needed run `php artisan serve` and navigate to localhost:8000/authors/create

Open the **create.blade.php**

Follow the tutorial

```php
@extends('layouts.app')

@section('content')
    <div class="w-2/3 bg-gray-200 mx-auto p-6 shadow">
        <form action="/authors" method="post" class="flex flex-col items-center">
            @csrf

            <h1>Add New Author</h1>

            <div class="pt-4">
                <input type="text" name="name" placeholder="Full Name" class="rounded px-4 py-2 w-64">
                @error('name') <p class="text-red-600">{{ $message }}</p> @enderror
            </div>
            <div class="pt-4">
                <input type="text" name="dob" placeholder="Date of Birth" class="rounded px-4 py-2 w-64">
                @error('dob') <p class="text-red-600">{{ $message }}</p> @enderror
            </div>
      1      <div class="pt-4">
                <button class="bg-blue-400 text-white rounded py-2 px-4">Add New Author</button>
            </div>
        </form>
    </div>
@endsection
```

Update the '.env' file

- Remove the mysql settings
- Add `DB_CONNECTION=sqlite`

```text
DB_CONNECTION=sqlite
```

Run artisan migrate

```sh
php artisan migrate
```

```text
Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table
Migrated:  2014_10_12_000000_create_users_table
Migrating: 2014_10_12_100000_create_password_resets_table
Migrated:  2014_10_12_100000_create_password_resets_table
Migrating: 2019_05_06_120614_create_books_table
Migrated:  2019_05_06_120614_create_books_table
Migrating: 2019_06_25_110242_create_authors_table
Migrated:  2019_06_25_110242_create_authors_table
Migrating: 2019_07_23_104204_create_reservations_table
Migrated:  2019_07_23_104204_create_reservations_table
```

Open the browser and navigate to the project <http://youtube.library.test/authors/create>

- Create an author

Navigate to the sqlite database

- F1 open sqlite database
  - select database.sqlite
- Sqlite explorer
  - expand authors
  - Click the run icon

```json
{
 "stmt": "SELECT * FROM `authors`;",
 "header": ["id", "name", "dob", "created_at", "updated_at"],
 "rows": [
  [
   "1",
   "Fred Bloggs",
   "1900-01-01 00:00:00",
   "2019-07-24 15:29:15",
   "2019-07-24 15:29:15"
  ]
 ]
}
```

The data has been added to the database.
