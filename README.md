# laravel-base-repository
A flexible Laravel repository pattern foundation for working with Eloquent ORM.

The goal of this package is to provide a foundation for building Laravel Eloquent repositories while still allowing you to create basic queries on the fly.

## Installation

Install this package through Compposer. Edit your project's composer.json file to require kyle-noland/laravel-base-repository

``` json
"require": {
    "kyle-noland/laravel-base-repository": "dev-master"
}
```

Update Composer from the Terminal

``` 
composer update
```

Add the Service Provider to your app/config/app.php file

``` php
'KyleNoland\LaravelBaseRepository\LaravelBaseRepositoryServiceProvider'
```

## Usage

Extend the BaseRepository class and implement your own custom repository logic:

``` php
<?php namespace MyProject\Repositories;

use KyleNoland\LaravelBaseRepository\BaseRepository;
use MyProject\Interfaces\CompanyRepositoryInterface;
use MyProject\Models\Company;

class CompanyRepository extends BaseRepository implements CompanyRepositoryInterface {

	public function __construct(Company $model)
	{
		$this->model = $model;
	}
	
	// Add your repository methods here

}
```

The BaseRepository class provides basic COUNT, SELECT, INSERT, UPDATE, DELETE, WHERE, WHERE IN clauses and the ability to eager load related models.

### Counting All Models

``` php
$count = $this->companyRepo->count();
```

### Counting a Subset of Models

``` php
$count = $this->companyRepo->where('is_active', true)->count();
```

### Selecting Models

``` php
$allCompanies = $this->companyRepo->all();
$activeCompanies = $this->companyRepo->where('is_active', true)->get();
$activeCopmaniesInTexas = $this->companyRepo->where('is_active', true)->where('state', 'TX')->get();
```
