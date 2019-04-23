# WPloadbalanced-Docker
To launch the project :
```bash
docker-compose up -d
```

Should return :
```bassh
Creating wploadbalanced-docker_db_1    ... done
Creating wploadbalanced-docker_adminer_1 ... done
Creating wploadbalanced-docker_wordpress_1 ... done
```

This `docker-compose.yml` load a fonctionnal load-balanced WP server

Name |Service | int port | exp port | depends |
-|-|-|-|-|
db | mariadb | 3306 | 3306 | `[]`|
adminer | adminer | 8080 | 8080 | `[db]`|
wordpress | wordpress | 80 | 8000 | `[db]` |

