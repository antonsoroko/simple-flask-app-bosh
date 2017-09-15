# simple-flask-app-bosh
## BOSH release task for simple flask application.

### Release workflow:

- Prepare blobs:
```
$ wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tgz -O /tmp/Python-2.7.11.tgz
$ bosh add blob /tmp/Python-2.7.11.tgz python_2.7
$ pip download -r src/python_2.7/requirements.txt --dest blobs/python_2.7/vendor/
$ pip download -r src/simpleflaskapp/requirements.txt --dest blobs/simpleflaskapp/vendor/
$ bosh -n upload blobs
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
- Set `director_uuid` and `net_id` in manifest.yml:
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
$ bosh vms simpleflaskapp-deployment
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
