# kubecerts

Shows TLS/SSL certificates info for hosts/ingresses.  

## Install

You will need [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed and working in your context for ingress queries. (TLDR; `kubectl get ingress -A`)

* generic Unix install
```console
git clone https://github.com/aaparmeggiani/kubecerts
make install
```

* macOS / Homebrew
```console
brew tap aaparmeggiani/repo  (homebrew-repo)
brew install kubecerts
```

## Usage
```console
kubecerts [hosts] | [options]
ops:
    -h, --help              this help
    -n, --namespace [ns]    namespace to query - default: current
    -A, --all-namespaces    query ingress in all namespaces
    -f, --file [filename]   read hosts from file, one host per line
    -o, --output [format]   [ table | list | verbose ] - default: table
    -v, --version           Prints the kubetail version
```

## Examples
```console
$ date
Fri  6 Dec 2019 19:30:00 GMT

$ kubecerts github.com letsencrypt.org expired.badssl.com
HOST                START                 EXPIRE                VERIFY
github.com          2018-05-08T00:00:00Z  2020-06-03T12:00:00Z  ok.
letsencrypt.org     2019-09-29T16:33:36Z  2019-12-28T16:33:36Z  ok.
expired.badssl.com  2015-04-09T00:00:00Z  2015-04-12T23:59:59Z  result: certificate has expired (10), continuing anyway.

$ kubecerts --all-namespaces
HOST                    START                 EXPIRE                VERIFY
api.mydomain.com        2019-10-03T07:56:55Z  2020-01-01T07:56:55Z  ok.
auth.mydomain.com       2019-09-22T13:18:11Z  2019-12-21T13:18:11Z  ok.
admin.mydomain.com      2019-09-22T13:18:11Z  2019-12-21T13:18:11Z  ok.
console.mydomain.com    2019-10-03T09:07:42Z  2020-01-01T09:07:42Z  ok.
developer.mydomain.com  2019-10-03T09:07:40Z  2020-01-01T09:07:40Z  ok.
mydomain.com            2019-09-22T13:18:11Z  2019-12-21T13:18:11Z  ok.
www.mydomain.com        2019-09-22T13:18:11Z  2019-12-21T13:18:11Z  ok.

$ kubecerts google.com --output list
>> google.com
*  subject: C=US; ST=California; L=Mountain View; O=Google LLC; CN=*.google.com
*  start date: Nov  5 07:46:16 2019 GMT
*  expire date: Jan 28 07:46:16 2020 GMT
*  issuer: C=US; O=Google Trust Services; CN=GTS CA 1O1
*  SSL certificate verify ok.

```

## Todo
* namespace column (when `--all-namespaces`)
* column filters
* `subject`, `issuer`,  `days to expire` columns
* add 


## License
MIT

alpine dependencies
bash
curl 
util-linux
*date doesn-t accept -f parameter