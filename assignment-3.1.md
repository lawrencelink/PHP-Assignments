# Assignment 3.1 - Why does this code look so good?

` php-login / 1-minimal / classes / login.php:125`
```php
//  this code is indented correctly
//  every statement is on its own line
//  the curly braces are on their own line and indented correctly under the function declaration

//
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

```php
// the code looks correctly formatted
// code is spaced for easy reading
// variables are given descriptive names
// comments are included to help understand what the code is doing
//

namespace Guzzle\Http;

use Guzzle\Common\Version;
use Guzzle\Stream\Stream;
use Guzzle\Common\Exception\InvalidArgumentException;
use Guzzle\Http\Mimetypes;

/**
 * Entity body used with an HTTP request or response
 */
class EntityBody extends Stream implements EntityBodyInterface
{
    /** @var bool Content-Encoding of the entity body if known */
    protected $contentEncoding = false;

    /** @var callable Method to invoke for rewinding a stream */
    protected $rewindFunction;

    /**
     * Create a new EntityBody based on the input type
     *
     * @param resource|string|EntityBody $resource Entity body data
     * @param int                        $size     Size of the data contained in the resource
     *
     * @return EntityBody
     * @throws InvalidArgumentException if the $resource arg is not a resource or string
     */
    public static function factory($resource = '', $size = null)
    {
        if ($resource instanceof EntityBodyInterface) {
            return $resource;
        }

        switch (gettype($resource)) {
            case 'string':
                return self::fromString($resource);
            case 'resource':
                return new static($resource, $size);
            case 'object':
                if (method_exists($resource, '__toString')) {
                    return self::fromString((string) $resource);
                }
                break;
            case 'array':
                return self::fromString(http_build_query($resource));
        }

        throw new InvalidArgumentException('Invalid resource type');
    }

    public function setRewindFunction($callable)
    {
        if (!is_callable($callable)) {
            throw new InvalidArgumentException('Must specify a callable');
        }

        $this->rewindFunction = $callable;

        return $this;
    }

    public function rewind()
    {
        return $this->rewindFunction ? call_user_func($this->rewindFunction, $this) : parent::rewind();
    }

    /**
     * Create a new EntityBody from a string
     *
     * @param string $string String of data
     *
     * @return EntityBody
     */
    public static function fromString($string)
    {
        $stream = fopen('php://temp', 'r+');
        if ($string !== '') {
            fwrite($stream, $string);
            rewind($stream);
        }

        return new static($stream);
    }

    public function compress($filter = 'zlib.deflate')
    {
        $result = $this->handleCompression($filter);
        $this->contentEncoding = $result ? $filter : false;

        return $result;
    }

    public function uncompress($filter = 'zlib.inflate')
    {
        $offsetStart = 0;

        // When inflating gzipped data, the first 10 bytes must be stripped
        // if a gzip header is present
        if ($filter == 'zlib.inflate') {
            // @codeCoverageIgnoreStart
            if (!$this->isReadable() || ($this->isConsumed() && !$this->isSeekable())) {
                return false;
            }
            // @codeCoverageIgnoreEnd
            if (stream_get_contents($this->stream, 3, 0) === "\x1f\x8b\x08") {
                $offsetStart = 10;
            }
        }
```