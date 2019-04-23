# WPloadbalanced-Docker

```bash
docker-compose up -d
```

This `docker-compose.yml` load a fonctionnal load-balanced WP server

Name |Service | int port | exp port | depends |
-|-|-|-|-|
db | mariadb | 3306 | 3306 | `[]`|
adminer | adminer | 8080 | 8080 | `[db]`|
wordpress | wordpress | 80 | 8000 | `[db]` |

