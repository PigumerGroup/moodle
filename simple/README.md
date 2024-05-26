
```text
mkdir /var/moodledata
```

```text
chown -R www-data:www-data /var/www/html/moodle
chown -R www-data:www-data /var/moodledata
```

```text
crontab -u www-data -e
```

```text
* * * * * /usr/bin/php /var/www/html/moodle/admin/cli/cron.php > /dev/null
```

## 参考

- [G Suite アカウントでログインできる Moodle 3.5.9+ を業務効率化のために導入した話](https://qiita.com/k-kana/items/0269d1f831483c39f3e7)
