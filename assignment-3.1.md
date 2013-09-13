# Assignment 3.1 - Why does this code look so good?

` php-login / 1-minimal / classes / login.php:125`
```php
//  this code is indented correctly
//  every statement is on its own line
//  the curly braces are on their own line and indented correctly under the function declaration

/**
     * perform the logout
     */
    public function doLogout()
    {
        $_SESSION = array();
        session_destroy();
        $this->user_is_logged_in = false;
        $this->messages[] = "You have been logged out.";

    }
```