# How to start tunnel for automation test in Pytest on [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=Pytest-tunnel)

If you want to run your an automation test in Pytest on LambdaTest using the tunnel and want to start the tunnel automatically in the script, you can use the follwing steps. You can refer to sample test repo [here](https://github.com/LambdaTest/pytest-selenium-sample).

## Steps

### Step 1: Download the LT tunnel binary from LT Dashboard

Go to your LambdaTest dashboard and click the configure tunnel button on the top right corner and use the download link to download the binary file. 

### Step 2: Code to run LT tunnel before test

In your `conftest.py` file, ensure that you have specified the username and accesskey and paste the following code (refer to `conftest.py` for full code) :

```python
import  subprocess

#start tunnel process
tunnel_process = subprocess.Popen(["./LT","--user",username,"--key",access_key],stdout=subprocess.DEVNULL,stderr=subprocess.STDOUT)

#leave rest of the configuration untouched

#In the fin function, end the process
def fin():
        #browser.execute_script("lambda-status=".format(str(not request.node.rep_call.failed if "passed" else "failed").lower()))
        if request.node.rep_call.failed:
            browser.execute_script("lambda-status=failed")
        else:
            browser.execute_script("lambda-status=passed")
            browser.quit()
        #end tunnel process
        tunnel_process.terminate()
```
### Step 3: Set tunnel capability to True

Add the following line in `conftest.py`:

```python
desired_caps['tunnel'] = True
```
### Step 4: Run your test

```bash
cd tests //navigate to tests directory
python sample_todo.py
```


# Links:

[LambdaTest Community](http://community.lambdatest.com/)

