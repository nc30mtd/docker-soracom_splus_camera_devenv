# docker-soracom_splus_camera_devenv
SORACOM S+ Cameraの開発環境コンテナ


## Usage

```
$ docker-compose build
$ docker-compose up -d
$ docker-compose exec devenv bash

コンテナ内で下記を実行
$ cd opt
$ ssh setup.sh
```

## Troubleshooting

### 404 Client Error: Not Found for url: https://pypi.org/simple/tflite-runtime/

requirement.txt内のL.53

```
tflite-runtime==2.1.0.post1
```

のインストールが失敗することがある．その場合下記のようなエラーメッセージが表示されるはず．


```
Exception:
Traceback (most recent call last):
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/basecommand.py", line 215, in main
    status = self.run(options, args)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/commands/install.py", line 353, in run
    wb.build(autobuilding=True)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/wheel.py", line 749, in build
    self.requirement_set.prepare_files(self.finder)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/req/req_set.py", line 380, in prepare_files
    ignore_dependencies=self.ignore_dependencies))
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/req/req_set.py", line 554, in _prepare_file
    require_hashes
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/req/req_install.py", line 278, in populate_link
    self.link = finder.find_requirement(self, upgrade)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/index.py", line 465, in find_requirement
    all_candidates = self.find_all_candidates(req.name)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/index.py", line 423, in find_all_candidates
    for page in self._get_pages(url_locations, project_name):
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/index.py", line 568, in _get_pages
    page = self._get_page(location)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/index.py", line 683, in _get_page
    return HTMLPage.get_page(link, session=self.session)
  File "/opt/soracom/python/lib/python3.6/site-packages/pip/index.py", line 795, in get_page
    resp.raise_for_status()
  File "/opt/soracom/python/share/python-wheels/requests-2.18.4-py2.py3-none-any.whl/requests/models.py", line 935, in raise_for_status
    raise HTTPError(http_error_msg, response=self)
requests.exceptions.HTTPError: 404 Client Error: Not Found for url: https://pypi.org/simple/tflite-runtime/
```

下記の通り対処する

- `requirement.txt` の L.53 をコメントアウトする

```
- tflite-runtime==2.1.0.post1
+ #tflite-runtime==2.1.0.post1
```

```
$ pip3 install https://dl.google.com/coral/python/tflite_runtime-2.1.0.post1-cp37-cp37m-linux_aarch64.whl
```