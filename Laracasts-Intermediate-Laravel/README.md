### Laravel Intermediate Level:
__Episode 1:__  Let's take a look at this file:
```
app\Console\Kernel.php
```
(This kernel is different from `app\Http\Kernel.php`.)

In this file, we can define `Cron jobs` and the method called `schedule()` is where we can schedule jobs for laravel to do, for example, sending an email on a specific time to the user, as the daily report.

Another example of this, is running an artisan command once a month, to delete old table records.

As we see by default, there is a command inside `schedule` method:
```
$schedule->command('inspire')
         ->hourly();
```
This is equivalent to say this hourly:
```
php artisan inspire
```
There is another way of scheduling tasks using `exec()` and some other helper commands:
```
protected function schedule(Schedule $schedule)
    {
        $schedule->exec("touch foo.txt")->everyFiveMinutes();
    }
```
There are more helpers like:
```
->everyTenMinutes()
->daily()
->dailyAt('10:30')
```
here is another example:
```
$schedule->command("laracasts:clear-history")->monthly();
$schedule->command("laracasts:daily-report")->dailyAt('23:55');
```
`laracasts:create-history` is customized for laracasts project.
There are more we can do with the command like:
```
$schedule->command("laracasts:clear-history")->monthly()
    ->sendOutputTo('/path/to/file')->emailOutputTo('mojiway@gmail.com');
```

