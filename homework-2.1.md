# Homework 2.1 - Ever wonder what all these signs say?


` php-login / 1-minimal / index.php:44`
    //Variable: $login
    //Comparison == equality
    //Function isUserLoggedIn()
`
```php
    if ($login->isUserLoggedIn() == true) {
    }
```

` php-login / 1-minimal / classes / login.php:128`
    //Function doLogout()
    //Variable $_SESSION
    //Assignment = 
    //Function session_destroy()
    //Variable $this
    //Array messages[]
`
```php    
public function doLogout()
    {
        $_SESSION = array();
        session_destroy();
        $this->user_is_logged_in = false;
        $this->messages[] = "You have been logged out.";

    }
```

` php-login / 1-minimal / classes / login.php:128`
    //Function _construct()
    //Function isset()
    //Variable $_POST
    //Variable $this
    //Function registerNewUser()
`
```php 
public function __construct()
    {

        if (isset($_POST["register"])) {

            $this->registerNewUser();

        }
    }
```