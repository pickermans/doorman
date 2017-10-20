# Doorman

- 서버에 컴포저 설치

    - https://www.lesstif.com/pages/viewpage.action?pageId=23757293#PHPComposer설치및사용법-Linux/Unix/MacOSX

- 프로젝트 루트 디렉토리로 이동

    - cd /var/www/my_project

- 아래명령어로 vendor디렉토리에 Doorman 패키지 설치

    - composer require asyncphp/doorman

- 패키지 설치 확인~

    - ls vendor

- 사용법

    - test.php

```php
error_reporting(E_ALL);
ini_set('display_errors', 1);

require 'vendor/autoload.php';

use AsyncPHP\Doorman\Manager\ProcessManager;
use AsyncPHP\Doorman\Task\ProcessCallbackTask;

$mytask = new ProcessCallbackTask(function () {
    shell_exec('ls -al');
});

$manager = new ProcessManager();

for($i=0; $i < 10; $i++) {
    $manager->addTask($mytask);
}


while ($manager->tick()) {
    usleep(250);
}
```

