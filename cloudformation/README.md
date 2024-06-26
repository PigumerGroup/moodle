Moodle
===

```text
;max_input_vars = 1000
```

```text
max_input_vars = 5000
```

```text
memory_limit = 40M
post_max_size = 80M
upload_max_filesize = 80M
```

## EFS

```text
$ sudo apt-get update
$ sudo apt-get -y install git binutils rustc cargo pkg-config libssl-dev
$ git clone https://github.com/aws/efs-utils
$ cd efs-utils
$ ./build-deb.sh
$ sudo apt-get -y install ./build/amazon-efs-utils*deb
```

```text
sudo mount -t efs file-system-id /mnt
```

/etc/fstab
```text
file-system-id:/ efs-mount-point efs _netdev,tls,iam 0 0
```

## moodledata

```text
sudo mkdir -p /mnt/moodledata
```

```text
sudo php /var/www/html/moodle/admin/cli/install.php
```

```text
chown -R www-data:www-data /var/www/html/moodle
chown -R www-data:www-data /mnt/moodledata
```

## crontab

```text
crontab -u www-data -e
```

```text
* * * * * /usr/bin/php /var/www/html/moodle/admin/cli/cron.php > /dev/null
```

```text
mysql -h HOST -u admin -p
```

```text
mysql> CREATE DATABASE moodle CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

```text
crontab -u www-data -e
```

```text
* * * * * /usr/bin/php /path/to/moodle/admin/cli/cron.php >/dev/null
```

## S3

```text
$CFG->alternative_file_system_class = '\tool_objectfs\s3_file_system';
```

## 参考

- [Moodle 4.4をAmazon EC2にインストールする](https://developer.mamezou-tech.com/blogs/2024/05/07/installing-moodle-on-aws/)
- [G Suite アカウントでログインできる Moodle 3.5.9+ を業務効率化のために導入した話](https://qiita.com/k-kana/items/0269d1f831483c39f3e7)
- [IAM 認証を使用してマウントする](https://docs.aws.amazon.com/ja_jp/efs/latest/ug/mounting-IAM-option.html)
- [efs-utils](https://github.com/aws/efs-utils)
