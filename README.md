# teletypeBD

С библиотекой `teletypeBD` становится возможным использовать любое сообщество из социальной сети ВКонтакте в роли базы данных. Конечно это далеко не полноценная база данных, но в ознакомительных целях вполне подходит.

И так, для начала устанавливаем модуль:
```py
>>> pip install teletypeBD
```

Далее создаем новый файл и импортируем главный класс из нашего модуля:
```py
from teletypeBD import Client
```

Добаляем токен от нашей страницы, и id сообщества, которое будет выступать в роли БД:
```py
client = Client("hfaa1c7c035cafe3bf8cececf7054g0e88d34c6d567jazhrpqbe877a0ad7228ed9a1a46b06a5b6bd14444", -209825229) # данные не действительные
```

Можно заносить как один токен, так и несколько:
```py
client = Client([
  "hfaa1c7c035cafe3bf8cececf7054g0e88d34c6d567jazhrpqbe877a0ad7228ed9a1a46b06a5b6bd14444",
  "fsdag2154n5dasredak432k5m45b5423n42315235h4535n13432k5m45b4321543kfsdkfsdafi432k5m45b",
  "5454kj54msadmnk13432k424msa4123a321423mdafsdagfdsaplzpppzqe,czxmweqrowk4kj1k54k454ytrs"
], -209825229)
```

**Обратите внимание что страницы, токены которых содержется в классе клиента, должны иметь права админа в группе которой также передаётся в классе клиента.**

И занесём пару записей в нашу БД:
```py
client.insert([
  {
    "_id": 1,
    "name": "hizri",
    "age": 16,
    "warns": []
  },
  {
    "_id": 2,
    "name": "gadji",
    "age": 17,
    "warns": [1, 2, 3]
  }
])
```

Давайте теперь попробуем сохранить в переменную `one` запись у которой айдишник равен `1`, и сохранить в перменную `two` записи у которых айдишники `1` и `2`:
```py
one = client.find({"_id": 1})

two = client.find({"_id": [1, 2]})

>>> Переменные one и two содержат списки с соответствующими значениями
```

А теперь давайте обновим у всех записей в бд ключ `name` на `no name`, а к ключам `age` прибавим значение `1`:
```py
client.update({
	"_id": [post["_id"] for post in client.find_all()]
}, {
	"$set": {"name": "no name"},
	"$inc": {"age": 1}
})
```

Думаю теперь стоит удалить все записи с БД:
```py
client.delete({"_id": "all"})
```
