# Demo Steps

```
laravel new 102
cd 102
subl .
// update db details
php artisan make:auth
php artisan migrate
php artisan serve
// do registration & login
php artisan make:controller UserController -r
	public function index()
    {
        $users = User::all();
        return view('users.index', compact('users'));
    }

    @extends('layouts.app')

	@section('content')
		<div class="container">
			<ul>
				@forelse($users as $user)
					<li>{{ $user->name }}</li>
				@empty
					<li>No users for now</li>
				@endforelse
			</ul>
		</div>
	@endsection

	Route::resource('users', 'UserController');

// exclude current user
$users = User::where('id', '!=', auth()->user()->id)->paginate();

php artisan tinker
factory(App\User::class, 100)->create();

// setup mailtrap
php artisan make:notification SendEmailDemo

// routes/console.php
Artisan::command('mail:me', function () {
    Auth::loginUsingId(1);
    Auth::user()->notify(new App\Notifications\SendEmailDemo());
})->describe('Display an inspiring quote');

php artisan mail:me

php artisan mail:me
```