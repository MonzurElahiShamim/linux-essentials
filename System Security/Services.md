
## To `start` a service:

```shell
# service service_name start 
service httpd start
```
or 
```shell
# systemctl start service_name
systemctl start httpd
```

## To `stop` a service:

```shell
# systemctl stop service_name
systemctl stop httpd
```

## To check `status` of a service:

```shell
# systemctl status service_name
systemctl status httpd
```

## To configure a service to `start at startup`:

```shell
# systemctl enable httpd
systemctl enable httpd
```

### To configure a service to `not start at startup`:

```shell
# systemctl disable service_name
systemctl disable httpd
```

