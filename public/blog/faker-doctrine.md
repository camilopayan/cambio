## Introduction

[Faker](https://github.com/fzaninotto/Faker) is a great PHP library for creating
realistic looking data for prototyping and validating your project. That project
might be using [Doctrine 2](http://www.doctrine-project.org/), which is a PHP
ORM for mapping your database tables to PHP objects in your code. If you're
using Doctrine, you'll want to use it to insert your fake data for testing or
prototyping.

## Using Faker with Doctrine

I'm assuming that at this point, you've already got Doctrine wired up to
whatever database you're using, and you're ready to fill your DB with fake data.

First, we'll install Faker using `composer require
fzaninotto/faker`.

Next, we'll make a `bootstrap_database.php` file that's going to need your
entity manager from Doctrine.

    <?php
	 require 'vendor/autoload.php';

	 use Doctrine\ORM\EntityManager;
	 use Doctrine\ORM\Tools\Setup;

	 $path = array('PATH TO YOUR ENTITIES');
	 $devMode = true;

	 $config = Setup::createAnnotationMetadataConfiguration($path, $devMode);

	 $dbParams = array(
	 	'driver'		=> 'pdo_mysql',
		'user'		=> 'YOUR DATABASE USERNAME',
		'password'	=> 'YOUR DATABASE PASSWORD',
		'dbname'		=> 'YOUR DATABASE NAME',
		'host'		=> 'YOUR DATABASE HOST'
	 );

	 $em = EntityManager::create($dbParams, $config);

If that looks familiar to you, that's because it's pretty vanilla setup code for
Doctrine. The next step is, of course, inserting our data using Faker. Let's
pretend we've got a User entity set up with the namespace `\App\Entity\User`.
The rest of our `bootstrap_database.php` file will look like this:

    //Create your Faker generator
    $generator = \Faker\Factory::create();

	 /* Give the Faker populator the EntityManager object from Doctrine, as well
	 *  as the Faker Generator
	 */
	 $populator = new Faker\ORM\Doctrine\Populator($generator, $em);
	 /* Make sure to use the fully qualified class name for your Entity, in this
	 *  case it's \App\Entity\User, and then tell Faker just how many of those
    *  you want. Here, we're making 5 users.
	 */
	 $populator->AddEntity('\App\Entity\User', 5);
	 
	 //You can store the fake data, as well.
	 $insertedFakeData = $populator->execute();

That's the long and short of it. Faker has filled your database with fake data. Faker will take a look at the metadata and names of your columns and
try to choose appropriate fake data to fill it with. For example, Faker will fill a column `name`
with real-looking names, not lorem ipsum.
