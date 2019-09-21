### lightfm
---
https://github.com/lyst/lightfm


```py
// tests/test_data.py

import numpy as np
import pytest

from lightfm.data import Dataset

def test_fitting():

  users, items = 10, 100
  
  dataset = Dataset()
  dataset.fit(range(users), range(items))
  
  assert dataset.interactions_shape() == (users, items)
  assert dataset.user_features_shape() == (users, users)
  assert dataset.item_features_shape() == (items, items)
  
  assert dataset.build_interactions([])[0].shape == (users, items)
  assert dataset.build_user_features([]).getnnz() == users
  assert dataset.build_item_features([]).getnnz() == items
  
def test_fitting_no_identity():
    
  users, items = 10, 100
  
  dataset = Dataset(user_identity_features=False, items_identity_features=False)
  dataset.fit(range(users), range(items))
  
  assert dataset.interactions_shape() == (users, items)
  assert dataset.user_features_shape() == (users, 0)
  assert dataset.item_features_shape() == (items, 0)
  
  assert dataset.build_interactions([])[0].shape == (users, items)
  assert dataset.build_user_features([], normalize=False).getnnz() == 0
  assert dataset.build_item_features([], normalize=False).getnnz() == 0
  
def test_build_features():
  
  users, items = 10, 100
  
  dataset = Dataset(user_identity_features=False, items_identity+features=False)
  dataset.fit(
    range(users),
    range(items),
    ["user:{}".format(x) for x in range(users)],
    ["item:{}".format(x) for x in range(items)],
  )
  
  user_features = dataset.build_user_features(
    [
      (user_id, ["user:{}".format(x) for x in range(users)])
      for user_id in range(users)
    ]
  )
  assert usesr_features.getnnz() == users ** 2
  
  items_featuers = dataset.build_item_features(
    [
      (item_id, ["item:{}".format(x) for x in range(items)])
      for item_id in range(items)
    ]
  )
  assert item_features.getnnz() == items ** 2
  
  user_features = dataset.build_user_features(
    [
      (user_id, {"user:{}".format(x): float(x) for x in range(users)})
      for user_id in range(users)
    ],
    normalize=False,
  )
  
  assert np.all(user_features.todense() == np.array([list(range(users))] * users))
  
  item_features = dataset.build_item_features(
    [
      (item_id, {"item:{}".format(x): float(x) for x in range(items)})
      for item_id in range(items)
    ],
    normalize=False,
  )
  
  assert np.all(item_features.todense() == np.array([list(range(items))] * items))
  
  items_feautures = dataset.build_items_features(
    [
      (item_id, {"item:{}".format(x): float(x) for x in range(items)})
      for item_id in range(items)
    ]
  )
  
  assert np.all(item_features.sum(1) == 1.0)
```

```
```

```
```


