

```python
#A Start
text=sc.textFile("/loudacre/devicestatus.txt")
```


```python
#A Review
text.take(2)
```




    [u'2014-03-15:10:10:20,Sorrento F41L,8cc3b47e-bd01-4482-b500-28f2342679af,7,24,39,enabled,disabled,connected,55,67,12,33.6894754264,-117.543308253',
     u'2014-03-15:10:10:20|MeeToo 1.0|ef8c7564-0a1a-4650-a655-c8bbd5f8f943|0|31|63|70|39|27|enabled|enabled|enabled|37.4321088904|-121.485029632']




```python
#B Start
temp = text.map(lambda val: val.split(val[19]))
```


```python
#C Start
filtertemp = temp.filter(lambda val : len(val) == 14)
```


```python
#B Test
temp.count()
```




    100000




```python
#C Test - OMG Same Count !
filtertemp.count()
```




    100000




```python
#D start
filtertemp.take(2) 
```




    [[u'2014-03-15:10:10:20',
      u'Sorrento F41L',
      u'8cc3b47e-bd01-4482-b500-28f2342679af',
      u'7',
      u'24',
      u'39',
      u'enabled',
      u'disabled',
      u'connected',
      u'55',
      u'67',
      u'12',
      u'33.6894754264',
      u'-117.543308253'],
     [u'2014-03-15:10:10:20',
      u'MeeToo 1.0',
      u'ef8c7564-0a1a-4650-a655-c8bbd5f8f943',
      u'0',
      u'31',
      u'63',
      u'70',
      u'39',
      u'27',
      u'enabled',
      u'enabled',
      u'enabled',
      u'37.4321088904',
      u'-121.485029632']]




```python
tempD = filtertemp.map(lambda arr : (arr[0],arr[1],arr[2],arr[12],arr[13]))
```


```python
tempD.take(2)
```




    [(u'2014-03-15:10:10:20',
      u'Sorrento F41L',
      u'8cc3b47e-bd01-4482-b500-28f2342679af',
      u'33.6894754264',
      u'-117.543308253'),
     (u'2014-03-15:10:10:20',
      u'MeeToo 1.0',
      u'ef8c7564-0a1a-4650-a655-c8bbd5f8f943',
      u'37.4321088904',
      u'-121.485029632')]




```python
#E start
tempE = filtertemp.map(lambda arr : (arr[0],arr[1].split(' ')[0],arr[2],arr[12],arr[13]))
```


```python
tempE.take(2)
```




    [(u'2014-03-15:10:10:20',
      u'Sorrento',
      u'8cc3b47e-bd01-4482-b500-28f2342679af',
      u'33.6894754264',
      u'-117.543308253'),
     (u'2014-03-15:10:10:20',
      u'MeeToo',
      u'ef8c7564-0a1a-4650-a655-c8bbd5f8f943',
      u'37.4321088904',
      u'-121.485029632')]




```python
#F Start
tempF = tempE.map(lambda val: ','.join(val))


```


```python
tempF.take(2)
```




    [u'2014-03-15:10:10:20,Sorrento,8cc3b47e-bd01-4482-b500-28f2342679af,33.6894754264,-117.543308253',
     u'2014-03-15:10:10:20,MeeToo,ef8c7564-0a1a-4650-a655-c8bbd5f8f943,37.4321088904,-121.485029632']




```python
tempF.saveAsTextFile("/loudacre/devicestatus_etl")
```


```python

```
