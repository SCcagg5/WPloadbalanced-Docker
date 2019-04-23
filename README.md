# WPloadbalanced-Docker
To launch the project :
```bash
docker-compose up -d --scale frontweb=2 --scale wordpress=2
```

Should return :
```bassh
Creating network "wploadbalanced-docker_back-tier" with driver "bridge"
Creating network "wploadbalanced-docker_admin-tier" with driver "bridge"
Creating network "wploadbalanced-docker_front-tier" with driver "bridge"
Creating wploadbalanced-docker_db_1 ... done
Creating wploadbalanced-docker_adminer_1   ... done
Creating wploadbalanced-docker_wordpress_1 ... done
Creating wploadbalanced-docker_wordpress_2 ... done
Creating wploadbalanced-docker_lb-admin_1  ... done
Creating wploadbalanced-docker_frontweb_1  ... done
Creating wploadbalanced-docker_frontweb_2  ... done
Creating wploadbalanced-docker_lb_1        ... done
```

This `docker-compose.yml` load a fonctionnal load-balanced WP server

Name |Service | int port | exp port | depends |
-|-|-|-|-|
db | Mariadb | 3306 | 3306 | `[]`|
adminer | Adminer | 8080 | 8080 | `[db]`|
frontweb | Wordpress | 80 | 32772+ | `[db]` |
lb | HAProxy | 80 | 80 | `[frontweb]` |

