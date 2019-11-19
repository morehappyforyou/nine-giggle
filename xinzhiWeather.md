# nine-giggle
import requests


class Weather(object):
    def __init__(self, city):
        self.appkey = "20unx0zpqgyl4ozc"
        self.city = city

    def get_data(self):

        url = "https://api.seniverse.com/v3/weather/now.json?location=" + self.city + "&key=20unx0zpqgyl4ozc"
        # _params = {"location": c, "key": self.appkey}
        r_air = requests.get(url, verify=True)
        con_air = r_air.json()
        # print(con_air)
        _text = con_air["results"][0]["now"]["text"]
        _code = con_air["results"][0]["now"]["code"]
        _temperature = con_air["results"][0]["now"]["temperature"]
        print("当前天气文字:", _text, "\n当前天气代码:", _code, "\n当前温度：" + _temperature)

    def weather_future(self):

        url = "https://api.seniverse.com/v3/weather/daily.json?location=" + self.city + \
              "&key=20unx0zpqgyl4ozc&unit=c&start=0&days=3"

        r_air = requests.get(url, verify=True)
        con_air = r_air.json()
        for i in range(3):
            _text_day = con_air["results"][0]["daily"][i]["text_day"]
            _code_day = con_air["results"][0]["daily"][i]["code_day"]
            _text_night = con_air["results"][0]["daily"][i]["text_night"]
            _code_night = con_air["results"][0]["daily"][i]["code_night"]
            _high = con_air["results"][0]["daily"][i]["high"]
            _low = con_air["results"][0]["daily"][i]["low"]
            _precip = con_air["results"][0]["daily"][i]["precip"]
            _wind_speed = con_air["results"][0]["daily"][i]["wind_speed"]
            _wind_scale = con_air["results"][0]["daily"][i]["wind_scale"]

            print("未来第" + str(i + 1) + "天天气：\n" + "天气：" + _text_day + "\n天气代码：" + _code_day +
                  "\n夜晚天气：" + _text_night + "\n夜晚天气代码：" + _code_night +
                  "\n最高温度：" + _high + "\n最低温度" + _low + "\n降水概率：" + _precip +
                  "\n风速" + _wind_speed + "\n风向" + _wind_scale)

    def life_index(self):
        url = "https://api.seniverse.com/v3/life/suggestion.json?key=20unx0zpqgyl4ozc&location=" + self.city\
              + "&language=zh-Hans"
        r_air = requests.get(url, verify=True)
        con_air = r_air.json()
        # print(con_air["results"][0]["suggestion"]["dressing"]["brief"])
        _dressing = con_air["results"][0]["suggestion"]["dressing"]["brief"]
        _sport = con_air["results"][0]["suggestion"]["sport"]["brief"]
        _uv = con_air["results"][0]["suggestion"]["uv"]["brief"]
        _travel = con_air["results"][0]["suggestion"]["travel"]["brief"]
        _car_washing = con_air["results"][0]["suggestion"]["car_washing"]["brief"]
        _flu = con_air["results"][0]["suggestion"]["flu"]["brief"]
        print("穿衣指数：", _dressing, "\n运动指数：", _sport,"\n紫外线强度：", _uv,
              "\n旅行指数：", _travel, "\n感冒指数：", _flu, "\n洗车指数：", _car_washing)
        # print(con_air)


if __name__ == '__main__':
    while True:
        c = input("Enter the city:")
        w = Weather(c)
        w.weather_future()
        w.life_index()
        w.get_data()
