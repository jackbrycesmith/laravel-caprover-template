<p align="center">
  <a href="https://github.com/laravel/laravel">
    <img src="https://avatars3.githubusercontent.com/u/958072?s=200&v=4" height="60">
  </a>
  +
  <a href="https://github.com/CapRover/CapRover">
    <img src="https://avatars0.githubusercontent.com/u/46361891?s=200&v=4" height="60">
  </a>
</p>
<h1 align="center">
  Laravel + CapRover
</h1>
<p align="center">
    Template to deploy a <a href="https://github.com/laravel/laravel">Laravel</a> app to a server managed by <a href="https://github.com/CapRover/CapRover">CapRover</a>.
</p>

<p align="center">
    <strong>
        <a href="https://jack.bryce-smith.com/💡/laravel-docker-caprover">jack.bryce-smith.com/💡/laravel-docker-caprover</a>
    </strong>
</p>

## Features

- 🐳 Lightweight [PHP 7.4](https://github.com/jackbrycesmith/laravel-caprover-template/blob/master/.deploy/Dockerfile#L1) image with [common extensions](https://github.com/jackbrycesmith/laravel-caprover-template/blob/master/.deploy/Dockerfile#L21); add/remove as required
- 📦 [Installs composer dependencies](https://github.com/jackbrycesmith/laravel-caprover-template/blob/master/.deploy/Dockerfile#L30); cached between builds if no changes
- ⚡️ Served via [Caddy 2](https://github.com/caddyserver/caddy)
- ⏰ [Setup to call](https://github.com/jackbrycesmith/laravel-caprover-template/blob/master/.deploy/Dockerfile#L11) the [Laravel command scheduler](https://laravel.com/docs/7.x/scheduling)
- 🛰 Straightforward websockets support
- 💪 [Services will restart](https://github.com/jackbrycesmith/laravel-caprover-template/blob/master/.deploy/config/supervisor.conf) thanks to [supervisord](https://github.com/ochinchina/supervisord)

## Usage

1. [Install Laravel](https://laravel.com/docs/7.x/installation#installing-laravel), e.g. `laravel new -f .`
2. <a href="https://jack.bryce-smith.com/💡/laravel-docker-caprover"><i>jack.bryce-smith.com/💡/</i>laravel-docker-caprover</a>
3. [Deploy to CapRover](https://caprover.com/docs/deployment-methods.html), e.g. `caprover deploy`
