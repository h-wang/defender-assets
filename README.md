# defender-assets
Defender rules for [Defender](https://github.com/h-wang/defender).
This way you can customize your own defender rules.

## How to use
```php
use Hongliang\Defender\Defender;
use Hongliang\Defender\Voter\IpRangeVoter;
use Hongliang\Defender\Voter\UriKeywordVoter;

$defender = new Defender();

$file = '[path to defender-assets/assets.php';
if (file_exists($file)) {
    $assets = require_once($file);

    $keywordVoter = new UriKeywordVoter();
    $keywordVoter->setAssets($assets['urikeywords']);

    $ipVoter = new IpRangeVoter();
    $ipVoter->setAssets($assets['iprange']);

    $defender->addVoter($ipVoter, Defender::FORBIDDEN)
        ->addVoter($keywordVoter, Defender::DENY);
} else {
    $defender->addVoter(new IpRangeVoter(), Defender::FORBIDDEN)
        ->addVoter(new UriKeywordVoter(), Defender::DENY);
}
$defender->react();
```
