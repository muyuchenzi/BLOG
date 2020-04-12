1、时间戳
time_stamp=time.time()#即为从1970.1.1到今天的所有秒数
2、时间戳转换为当前时间
time_localtime=time.localtime(time.time())
转换后的时间是个struct_time格式文件如果想从新转回time.time()
struct_time是一个多个元素构成的tuple 包括年月日，小时分钟秒，还有当前星期、今年的天数等等信息
所以需要从struct_time 拿到年月日，时分秒，
get_now_time=datetime.datetime(*struct_time[:6])
time.mktime()args需要转换成timetuple()
然后time_stamp=time.mktime(get_now_time.timetuple())

3、字符串转换成datetime
datetime_string='1999-9-9'
通过
datetime_result=datetime.datetime.strptime(datatime_string,'%Y/%m/%d')

4、datetime转换成str
datetime_today=datetime.datetime.today()
datetime_string=datetime.datetime.strftime(datetime_today)

5、datetime计算时间间隔
date_now=datetime.datetime.today()
date_time_delta=datetime.timedelta(days=500)
date_time_500days_ago=date_now-date_time_delta
#转换成字符串
string_500_ago=datetime.datetime.strftime(date_time_500days_ago,'%Y-%m-%d')



import time
import datetime

# 时间戳转换成datetime然后转回来
print('-----------------时间戳转换成datetime然后转换回来')
time_stamp = time.time()

print(time.localtime(time_stamp))
struct_my_time = time.localtime(time_stamp)
print(datetime.datetime(*struct_my_time[:6]))
get_now_time = datetime.datetime(*struct_my_time[:6])
print(time.mktime(get_now_time.timetuple()))

# 字符串转换成datetime
print('--------------字符串转换成datetime------------------')
datetime_string = '1999-9-9'
date_time_my = datetime.datetime.strptime(datetime_string, '%Y-%m-%d')
print(type(date_time_my))
print(date_time_my.strftime('%Y/ %m/%d'))

# datetime转换成字符串
print('--------------datetime转换成字符串--------------------')
date_time = datetime.datetime.today()
date_time_ymd = datetime.datetime.strftime(date_time, '%Y-%m-%d')
print(type(date_time_ymd))

# 计算时间间隔
print('-----------计算时间间隔-----------------')
date_time_my_1 = datetime.datetime.now()
date_time_my_ymd = datetime.datetime.strftime(date_time_my_1, '%Y-%m-%d')

print(type(date_time_my_ymd))
# 500天之前
date_time_delta = datetime.timedelta(days=500)
five_hundred_day_ago = date_time_my_1 - date_time_delta
print(five_hundred_day_ago)

