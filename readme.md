# Nova Assertions

Perform Nova requests & assert fields & authorization

### Installation

```
composer require dillingham/nova-assertions
```
```php
use NovaTesting\NovaAssertions;

class UserTest extends TestCase
{
    use NovaAssertions;

    public function testNova()
    {
        $this->be(factory(User::class)->create());

        $this->novaIndex('users')
            ->assertCanUpdate()
            ->assertCannotDelete()
            ->assertFieldsInclude('email')
            ->assertFieldsExclude('password');
    }
}
```

### Authentication
Log in a user that **[has access to Nova](https://nova.laravel.com/docs/2.0/installation.html#authorizing-nova)**
```php
$this->be(factory(User::class)->create());
```

### Requests

Request Nova's results with one of the following:

```php
$this->novaIndex($resource)
$this->novaDetail($resource, $id)
$this->novaCreate($resource)
$this->novaEdit($resource, $id)
```

TODO:: Add filtering & query params
->novaIndex('posts', [
    Filter::class => 'value'
]);

TODO: Add other requests to index & detail
Index requests filters & cards etc
So should ->novaIndex. Store as $cardResponse for assertions

### Assert Http
You can call **[http response methods](https://laravel.com/docs/5.8/http-tests#available-assertions)** as usual:

```php
$response->assertOk();
```

### Assert Fields

Assert columns or form fields with the following:

```php
$response->assertFieldsInclude('id');
$response->assertFieldsInclude('id', $user->id);
$response->assertFieldsInclude(['id', 'email']);
$response->assertFieldsInclude(['id' => 1, 'email' => 'example']);
$response->assertFieldsInclude('id', $users->pluck('id));
```
```php
$response->assertFieldsExclude('id');
$response->assertFieldsExclude('id', $user->id);
$response->assertFieldsExclude(['id', 'email']);
$response->assertFieldsExclude(['id' => 1, 'email' => 'example']);
$response->assertFieldsExclude('id, $users->pluck('id));
```

### Assert Actions

Coming soon

### Assert  Cards

Coming soon

### Assert Authorization

The following assert against the auth user & **[Nova's use of policies](https://nova.laravel.com/docs/2.0/resources/authorization.html#authorization)**

```php
$response->assertCanView();
$response->assertCanUpdate();
$response->assertCanDelete();
$response->assertCanForceDelete();
$response->assertCanRestore();
```
```php
$response->assertCannotView();
$response->assertCannotUpdate();
$response->assertCannotDelete();
$response->assertCannotForceDelete();
$response->assertCannotRestore();
```