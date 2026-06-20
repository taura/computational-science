# computational-science

## Wisteria

```
curl https://pyenv.run | bash
```

```
# ~/.bashrc に追記
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

```
# 好きなバージョンを入れる
pyenv install 3.14.6
```


```
# 3.14.6 のPythonでvenvを作る
/work/gt69/share/taura/pyenv/versions/3.14.6/bin/python -m venv /work/gt69/share/taura/venv/wisteria

# venvに入る
. /work/gt69/share/taura/venv/wisteria/bin/activate

# 必要なものを入れる
pip install ipykernel python-dotenv
pip install --upgrade git+ssh://git@github.com/UTokyo-IPP/ai-tutor-hey

# kernel登録
. /work/gt69/share/taura/venv/wisteria/bin/activate
python -m ipykernel install --user --name "wisteria" --display-name "Python 3.14 (wisteria)"
```

