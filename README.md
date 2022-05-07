![Composer Intro](assets/Title.png)

---

Creating a composer package is a straightforward and simple process. In this tutorial, we will be creating a simple composer package and deploying it to [Packagist](https://packagist.org/). A learning assignment will also be provided to challenge you to create a more complex composer package.

Estimated completion time: 20 - 30 minutes
This set of instructions is intended for beginners with a little experience with PHP, object oriented programming, and consuming a RESTful API.

## Contents
- [Intro - Basics of Making a Package](#intro---basics-of-making-a-package)
  - [Create Accounts](#create-accounts)
  - [Initialize Your Package](#initialize-your-package)
  - [File Structure Explained](#file-structure-explained)
  - [Writing our Package's Code](#writing-our-packages-code)
  - [Setting Up the Package Repository](#setting-up-the-package-repository)
  - [Submit the Package to Packagist](#submit-the-package-to-packagist)
- [Assignment - Build Your Own Package](#assignment---build-your-own-package)
  - [Requirements](#requirements)
  - [Class Diagram](#class-diagram)
  - [Key Challenges](#key-challenges)
  - [The Solution](#the-solution)

## Prerequisites
A basic understanding of PHP syntax, object oriented programming, and RESTful APIs.

## Objectives
- [ ] Learn what a composer package is.
- [ ] Learn what Packagist is.
- [ ] Learn how to deploy a composer package to Packagist.
- [ ] Learn how to implement a simple package with dependencies.

# Intro - Basics of Making a Package

## Create Accounts

Packagist is the main Composer repository for PHP packages. It aggregates all public PHP packages that are installable with Composer.

Since the end goal of this tutorial is to create a package and make it publicly available, we will need to create a GitHub and Packagist account to deploy our package.

If you haven't before, you can create an account on GitHub by following the instructions on the GitHub website at [https://github.com/](https://github.com/).

*Fun fact, if you haven't before, checkout the [GitHub Student Pack](https://education.github.com/pack)--It is a great learning resource.*

After that, create a Packagist account at [https://packagist.org/](https://packagist.org/). You can do this by going to the Packagist website and clicking on the "Sign up" button. We won't be using the account just yet, but we will need it later.

*Note: Keep track of your Packagist username, it will be used in the next step.*


## Initialize Your Package

It is time to start creating out package. To create package, you need to setup your package directory and initialize your package with a `composer.json` file. The` composer.json` is the file where your packge information is stored. To do that, you can run he following commands.

1. On your local machine, create a directory for your package and check into it.
```bash
mkdir my-package
cd my-package
```

2. Initialize your package with a `composer.json` file and default file structure.
```bash
composer init
```

Here, you should use your Packagist username as the vendor name (e.g. `liererkt`) followed by the package name (e.g. `my-package`) seperated by a `/`. This should look like `liererkt/my-package`. See the example output for more details.

*Note: the vendor name does not have to be your Packagist username, this will just make it easier to keep track of things.*

<details>
<summary>Example Output</summary>

```bash
Package name (<vendor>/<name>) [ubuntu/package]: liererkt/my-first-package
Description []: This is my first package!
Author [Kyle Lierer <liererkt@miamioh.edu>, n to skip]: 
Minimum Stability []: 
Package Type (e.g. library, project, metapackage, composer-plugin) []: project
License []: MIT

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]? no
Would you like to define your dev dependencies (require-dev) interactively [yes]? no
Add PSR-4 autoload mapping? Maps namespace "Liererkt\MyFirstPackage" to the entered relative path. [src/, n to skip]: 

{
    "name": "liererkt/my-first-package",
    "description": "This is my first package!",
    "type": "project",
    "license": "MIT",
    "autoload": {
        "psr-4": {
            "Liererkt\\MyFirstPackage\\": "src/"
        }
    },
    "authors": [
        {
            "name": "Kyle Lierer",
            "email": "liererkt@miamioh.edu"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]? yes
Generating autoload files
Generated autoload files
PSR-4 autoloading configured. Use "namespace Liererkt\MyFirstPackage;" in src/
Include the Composer autoloader with: require 'vendor/autoload.php';
```

</details>


## File Structure Explained

Before diving into the actual code, let's take a look at the file structure of our package. The file structure is as follows:

```
vendor/
├─ composer/
├─ autoload.php
src/
composer.json
```

* `vendor/`: This is where all of our dependencies are stored.
* `src/`: This is where our code is stored.
* `composer.json`: This is where our package information is stored.

## Writing our Package's Code

Now that we have our package directory and our `composer.json` file, we can start writing our code. We will start by creating a `src/Hello.php` file. This will serve as the entry point for our package. 

Then, we are going to add some simple test code to our `src/Hello.php` file and then we will come back later to add more functionality after we have deployed it once to Packagist.

1. Check into the `src/` directory.
```bash
cd src
```

2. Create a `Hello.php` file.
```bash
touch Hello.php
```

3. Add the following code to the `Hello.php` file.
```php
<?php 

/*
 * (c) Your Name <your email>
 *
 * This source file is subject to the MIT license that is bundled
 * with this source code in the file LICENSE.
 */

namespace liererkt\MyFirstPackage;

class Hello
{
    public function say($name)
    {
        return "Hello, $name!";
    }
}

?>
```

## Setting Up the Package Repository

In order to deploy our package, we will make use a GitHub repository. We will use the GitHub API and a webhook to trigger our package to be deployed. First, make a new empty GitHub repository with no files.

1. After creating your empty on GitHub, repository, Initialize your local repository.
```bash
git init
git remote add origin git@github.com:<your username>/<your project name>.git
```

2. Create a `.gitignore` file and add the vendor directory to it.
```bash
touch .gitignore
echo "vendor/" >> .gitignore
```

3. Commit the changes.
```bash
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
```

## Submit the Package to Packagist

Now that we have the package ready, we can submit it to Packagist.

1. Go to your [Packagist account settings](https://packagist.org/profile/edit) and select the "Connect to GitHub" option. This is so your Packagist account can access your GitHub account and be able to deploy your package.

2. Go to the Packagist home page and click on the "Submit a Package" button.

3. Fill out the form with your GitHub repository URL and click on the "Submit" button.

4. Congratulations! Your package is now available on Packagist and will update when you push to your GitHub repository.
  
*Note: Packagist determines the stability of your package based on the GIT tag. By default it will be dev. Thus, to require it, you'll need to specify the branch and dev like: `composer require liererkt/my-first-package:dev-main`. For instance, the command `git tag v1.0.0` will mark your branch as stable.*


# Assignment - Build Your Own Package

While we have a simple package created, we can do a lot more with it. For the sake of this tutorial, we will modify our existing package to be a simple PHP wrapper for the OpenWeatherAPI. Based on the following requirements, create your own more complex package.

## Requirements

Create a PHP wrapper for the OpenWeatherAPI that has the following features:
- [ ] A client that can be used to make `getCurrentWeather` requests to the OpenWeatherAPI.
- [ ] Model classes for OpenWeather request/response objects.
  - [ ] WeatherDay
  - [ ] Location

By the end of the assignment, you should have three classes (or similar classes):
 * OpenWeatherClient
 * WeatherDay
 * Location

*Note, it is recommended to follow the class diagram below (though this is not required)*

## Class Diagram
![Class Diagram](assets/Package-Diagram.svg)

## Key Challenges

- [ ] Adding a Guzzle/HTTP client to our package
- [ ] Determining how to handle the API key
- [ ] How to handle multiple classes in a single package
- [ ] How to handle error handling

## The Solution

While it is recommended to follow the class diagram above and build your own package yourself, there is a provided solution you can look if you finish and want to see another solution or you get stuck. To see the solution, select the `solution` branch of the repository.