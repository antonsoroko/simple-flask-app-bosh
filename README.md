# simple-flask-app-bosh
##BOSH release task for simple flask application.

###Release workflow:

- Prepare blobs:
```
$ cd /tmp
$ wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tgz
$ wget https://pypi.python.org/packages/py2.py3/w/wheel/wheel-0.29.0-py2.py3-none-any.whl
$ wget https://pypi.python.org/packages/py2.py3/p/pip/pip-8.1.1-py2.py3-none-any.whl
$ wget https://pypi.python.org/packages/py2.py3/s/setuptools/setuptools-20.9.0-py2.py3-none-any.whl
$ wget https://pypi.python.org/packages/py2.py3/v/virtualenv/virtualenv-15.0.1-py2.py3-none-any.whl
$ bosh add blob /tmp/pip-8.1.1-py2.py3-none-any.whl python_2.7
$ bosh add blob /tmp/wheel-0.29.0-py2.py3-none-any.whl python_2.7
$ bosh add blob /tmp/setuptools-20.9.0-py2.py3-none-any.whl python_2.7
$ bosh add blob /tmp/virtualenv-15.0.1-py2.py3-none-any.whl python_2.7
$ bosh add blob /tmp/Python-2.7.11.tgz python_2.7
```
- Create dev release:
```
bosh create release --force
```
- Target a director:
```
$ bosh target
$ bosh target <director_url>
```
- Set director_uuid and net_id in manifest.yml:
```
$ vim manifest.yml
```
- Choose deployment:
```
$ bosh deployments
$ bosh deployment manifest.yml
```
- Upload the new dev release:
```
$ bosh upload release
```
- Deploy dev release:
```
$ bosh deploy
```
- Check if everithing is fine
```
$ curl 10.10.10.48:8080/datetime
{
  "datetime": "2016-04-20 17:52:11.496375"
}
```
- Upload blobs:
```
$ bosh upload blobs
```
- Final release:
```
$ bosh create release --final
```
- Upload the new final release:
```
$ bosh upload release
```
- Deploy final release:
```
$ bosh deploy
```
