<p align=center>
  <br>
  <a href="https://sherlock-project.github.io/" target="_blank"><img src="https://user-images.githubusercontent.com/27065646/53551960-ae4dff80-3b3a-11e9-9075-cef786c69364.png"/></a>
  <br>
  <span>Hunt down social media accounts by username across <a href="https://github.com/sherlock-project/sherlock/blob/master/sites.md">social networks</a></span>
  <br>
  <a target="_blank" href="https://www.python.org/downloads/" title="Python version"><img src="https://img.shields.io/badge/python-%3E=_3.6-green.svg"></a>
  <a target="_blank" href="LICENSE" title="License: MIT"><img src="https://img.shields.io/badge/License-MIT-blue.svg"></a>
  <a target="_blank" href="https://github.com/sherlock-project/sherlock/actions" title="Test Status"><img src="https://github.com/sherlock-project/sherlock/workflows/Tests/badge.svg?branch=master"></a>
  <a target="_blank" href="https://github.com/sherlock-project/sherlock/actions" title="Nightly Tests"><img src="https://github.com/sherlock-project/sherlock/workflows/Nightly/badge.svg?branch=master"></a>
  <a target="_blank" href="https://twitter.com/intent/tweet?text=%F0%9F%94%8E%20Find%20usernames%20across%20social%20networks%20&url=https://github.com/sherlock-project/sherlock&hashtags=hacking,%20osint,%20bugbounty,%20reconnaissance" title="Share on Twitter"><img src="https://img.shields.io/twitter/url/http/shields.io.svg?style=social"></a>
  <a target="_blank" href="http://sherlock-project.github.io/"><img alt="Website" src="https://img.shields.io/website-up-down-green-red/http/sherlock-project.github.io/..svg"></a>
  <a target="_blank" href="https://hub.docker.com/r/theyahya/sherlock"><img alt="docker image" src="https://img.shields.io/docker/v/theyahya/sherlock"></a>
</p>

<p align="center">
  <a href="#installation">Installation</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#usage">Usage</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#docker-notes">Docker Notes</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#contributing">Contributing</a>
</p>

<p align="center">
<a href="https://asciinema.org/a/223115">
<img src="./images/sherlock_demo.gif"/>
</a>
</p>


## Instala????o

```console
git clone https://github.com/sherlock-project/sherlock.git
cd sherlock
```

# instale os requisitos

```
python3 -m pip install -r requirements.txt
```

## Uso

```console
$ python3 sherlock --help
usage: sherlock [-h] [--version] [--verbose] [--folderoutput FOLDEROUTPUT]
                [--output OUTPUT] [--tor] [--unique-tor] [--csv]
                [--site SITE_NAME] [--proxy PROXY_URL] [--json JSON_FILE]
                [--timeout TIMEOUT] [--print-all] [--print-found] [--no-color]
                [--browse] [--local]
                USERNAMES [USERNAMES ...]

Sherlock: encontrar nomes de usu??rio em redes sociais (Version 0.14.2)

  USERNAMES            Um ou mais nomes de usu??rio para verificar nas redes sociais.
                        Verifique nomes de usu??rio semelhantes usando{%} (replace to '_', '-', '.').

optional arguments:
  -h, --help           mostre esta mensagem de ajuda e saia
  --version             Exibe informa????es de vers??o e depend??ncias.
  --verbose, -v, -d, --debug
                        Exiba informa????es e m??tricas extras de depura????o.
  --folderoutput FOLDEROUTPUT, -fo FOLDEROUTPUT
                       Se estiver usando v??rios nomes de usu??rio, a sa??da dos resultados ser??
                       salvo nesta pasta.
  --output OUTPUT, -o OUTPUT
                       Se estiver usando um ??nico nome de usu??rio, a sa??da do resultado ser?? salva
                        a este arquivo.
  --tor, -t             Fa??a requisi????es pelo Tor; aumenta o tempo de execu????o; requer que o Tor seja
                       instalado e no caminho do sistema.
  --unique-tor, -u      Fa??a solicita????es pelo Tor com o novo circuito Tor ap??s cada solicita????o;
                        aumenta o tempo de execu????o; requer que o Tor esteja instalado e no sistema
                        caminho.
  --csv                 Crie um arquivo de valores separados por v??rgula (CSV).
  --xlsx               Crie o arquivo padr??o para o Microsoft Excel moderno
                        spreadsheet (xslx).
  --site SITE_NAME      Limit analysis to just the listed sites. Add multiple options to
                        specify more than one site.
  --proxy PROXY_URL, -p PROXY_URL
                        Make requests over a proxy. e.g. socks5://127.0.0.1:1080
  --json JSON_FILE, -j JSON_FILE
                        Load data from a JSON file or an online, valid, JSON file.
  --timeout TIMEOUT     Time (in seconds) to wait for response to requests (Default: 60)
  --print-all           Output sites where the username was not found.
  --print-found         Output sites where the username was found.
  --no-color            Don't color terminal output
  --browse, -b          Browse to all results on default browser.
  --local, -l           Force the use of the local data.json file.
```

To search for only one user:
```
python3 sherlock user123
```

To search for more than one user:
```
python3 sherlock user1 user2 user3
```

Accounts found will be stored in an individual text file with the corresponding username (e.g ```user123.txt```).

## Anaconda (Windows) Notes

If you are using Anaconda in Windows, using 'python3' might not work. Use 'python' instead.

## Docker Notes

If docker is installed you can build an image and run this as a container.

```
docker build -t mysherlock-image .
```

Once the image is built, sherlock can be invoked by running the following:

```
docker run --rm -t mysherlock-image user123
```

The optional ```--rm``` flag removes the container filesystem on completion to prevent cruft build-up. See: https://docs.docker.com/engine/reference/run/#clean-up---rm

The optional ```-t``` flag allocates a pseudo-TTY which allows colored output. See: https://docs.docker.com/engine/reference/run/#foreground

Use the following command to access the saved results:

```
docker run --rm -t -v "$PWD/results:/opt/sherlock/results" mysherlock-image -o /opt/sherlock/results/text.txt user123
```

The ```-v "$PWD/results:/opt/sherlock/results"``` options tell docker to create (or use) the folder `results` in the
present working directory and to mount it at `/opt/sherlock/results` on the docker container.
The `-o /opt/sherlock/results/text.txt` option tells `sherlock` to output the result.

Or you can use "Docker Hub" to run `sherlock`:
```
docker run theyahya/sherlock user123
```

### Using `docker-compose`

You can use the `docker-compose.yml` file from the repository and use this command:

```
docker-compose run sherlock -o /opt/sherlock/results/text.txt user123
```

## Contributing
We would love to have you help us with the development of Sherlock. Each and every contribution is greatly valued!

Here are some things we would appreciate your help on:
- Addition of new site support ??
- Bringing back site support of [sites that have been removed](removed_sites.md) in the past due to false positives

[1] Please look at the Wiki entry on [adding new sites](https://github.com/sherlock-project/sherlock/wiki/Adding-Sites-To-Sherlock)
to understand the issues.

## Tests

Thank you for contributing to Sherlock!

Before creating a pull request with new development, please run the tests
to ensure that everything is working great.  It would also be a good idea to run the tests
before starting development to distinguish problems between your
environment and the Sherlock software.

The following is an example of the command line to run all the tests for
Sherlock.  This invocation hides the progress text that Sherlock normally
outputs, and instead shows the verbose output of the tests.

```
$ cd sherlock/sherlock
$ python3 -m unittest tests.all --verbose
```

Note that we do currently have 100% test coverage.  Unfortunately, some of
the sites that Sherlock checks are not always reliable, so it is common
to get response problems.  Any problems in connection will show up as
warnings in the tests instead of true errors.

If some sites are failing due to connection problems (site is down, in maintenance, etc)
you can exclude them from tests by creating a `tests/.excluded_sites` file with a
list of sites to ignore (one site name per line).

## Stargazers over time

[![Stargazers over time](https://starchart.cc/sherlock-project/sherlock.svg)](https://starchart.cc/sherlock-project/sherlock)

## License

MIT ?? Sherlock Project<br/>
Original Creator - [Siddharth Dushantha](https://github.com/sdushantha)
