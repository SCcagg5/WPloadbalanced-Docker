# WPloadbalanced-Docker
To launch the project :
```bash
docker-compose up -d --scale front-web=2 --scale systm-wps=2 
```

Should return :
```bassh
Creating network "wploadbalanced-docker_back-net" with driver "bridge"
Creating network "wploadbalanced-docker_admin-net" with driver "bridge"
Creating network "wploadbalanced-docker_front-net" with driver "bridge"
Creating wploadbalanced-docker_datab-wps_1 ... done
Creating wploadbalanced-docker_front-adm_1 ... done
Creating wploadbalanced-docker_systm-wps_1 ... done
Creating wploadbalanced-docker_systm-wps_2 ... done
Creating wploadbalanced-docker_loadb-adm_1 ... done
Creating wploadbalanced-docker_front-web_1 ... done
Creating wploadbalanced-docker_front-web_2 ... done
Creating wploadbalanced-docker_loadb-web_1 ... done
```

This `docker-compose.yml` load a fonctionnal load-balanced WP server

Name |Service | int port | exp port | depends |
-|-|-|-|-|
datab-wps | Mariadb | `[3306]` | `[ / ]` | `[ / ]`|
systm-wps | Wordpress | `[9000]` | `[ / ]` | `[db]` |
front-adm | Adminer | `[8080]` | `[ / ]` | `[db]`|
front-web | Wordpress | `[9000]` | `[ / ]` | `[db, systm-wps]` |
loadb-adm | HAProxy | `[8080]` | `[8080, 443]` | `[db, front-adm]` |
loadb-web | HAProxy | `[80, 443]` | `[80, 443]` | `[db, systm-wps, front-web]` |

Network | Services | Purpose |
-|-|-|
back-net | datab-wps, systm-wps, front-adm, front-web | network between all back's services |
admin-net | front-adm, loadb-adm | expose adm web `:8080` |
front-net | front-web, loadb-web | expose usr web `:80, :443` |
