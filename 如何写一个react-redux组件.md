#### 如何写一个react-redux组件

##### 1. 设计数据结构

   1. 组件所显示的数据来自该数据结构。
   2. 该数据结构将挂在初始的state上面，如果为空，可设置为各种数据类型的初始化值。
   3. 思考该数据会有哪些操作，一般有：增加，更新，删除。

			{
				weather: {
					wendu: 23,
					shidu: 87,
					tip: 'good for everything'
				}
			}

##### 2. 根据数据结构操作写ActionTypes和Actions
1. 为该组件建立一个独立文件夹。
2. 创建actionTypes.js和actions.js。
3. 创建该数据结构对应的操作。
		
		//action types
		export const UPDATE_WEATHER = 'UPDATE_WEATHER';

		//actions
		import * as ActionTypes from './actionTypes';
		export const updateWeather = (data) => {
		    return {
		        type: ActionTypes.UPDATE_WEATHER,
		        data
		    }
		}
	
##### 3. 根据Actions写Reducer
1. 创建reducer.js。
2. 根据actions写出对应的处理方法。

		import * as ActionTypes from './actionTypes';
		export default (weather = {}, action) => {
		    switch(action.type) {
		        case ActionTypes.UPDATE_WEATHER:
		            return action.data;
		        default:
		            return weather;
		    }
		}

##### 4. 根据数据结构开发纯组件

   2. 创建组件文件view.js。
   3. 引入React，写一个包含render方法的组件。
   4. 根据此前设计的数据结构，给需要读取的属性取一个名字，该属性就是此前设计的数据结构。
   5. 在组件中读取该数据结构的各种数据，用于在页面中显示。

			render() {
		        const { weather } = this.props;
		        return (
		            <div>
		                <input type="search" value={this.state.search} onChange={this.onChange}/>
		                <button onClick={this.onSearch}>Search</button>
		                <div>
		                    <h4>{weather ? weather.city : 'loading...'}</h4>
		                    <div>{`温度：${weather ? weather.data.wendu : 'loading'}`}</div>
		                    <div>{`湿度：${weather ? weather.data.shidu : 'loading'}`}</div>
		                    <div>{`空气质量：${weather ? weather.data.quality : 'loading'}`}</div>
		                    <div>{`PM2.5：${weather ? weather.data.pm25 : 'loading'}`}</div>
		                    <div>{`温馨提醒：${weather ? weather.data.ganmao : 'loading'}`}</div>
		                </div>
		            </div>
		        )
		    }

##### 5. 开发container组件

   1. 定义mapStateToProps和mapDispatchToProps函数。创建一些用于读取和操作的属性，这些属性会传入组件中。例如以下的weather属性为一个值，updateWeather属性为一个函数，用于派发action。

			import Weather from './view';
			import { connect } from 'react-redux';
			import * as Actions from './actions';

			const mapStateToProps = (state) => {
			    return {
			        weather: state.weather,
			    }
			}
		
	        const mapDispatchToProps = (dispatch) => {
			    return {
			        updateWeather: (city) => dispatch(Actions.fetchWeather(city))
			    }
			}
			export default connect(mapStateToProps, mapDispatchToProps)(Weather);


​
##### 6. 创建出口文件
 
1. 创建index.js文件。
2. 将container.js,actions.js,reducer.js中的出口导出。
3. 以上便完成了一个独立的组件的开发，接下来就可以导入该组件了。

		import View from './container';
		import * as Actions from './actions';
		import Reducer from './reducer';
		
		export {
		    View,
		    Actions,
		    Reducer,
		}

##### 7.导入该组件

   1. 将数据结构名称与组件reducer对应，即该数据由该reducer处理。
   2. 为该数据结构赋值初始状态。
   3. 在需要引用该组件的地方，引用该组件。
   4. 全局只能有一个reducer，所以需要使用`combineReducers({data: dataReducer})`将所有reducer组合到一起。
   5. 使用`createStore(reducer, initState, applyMiddleware())`方法生成store,并传入Provider组件中。
   6. 在需要使用中间件时，需要使用applyMiddleware方法，并在创建store时传入。
		
			import { createStore, combineReducers, applyMiddleware } from 'redux';
			import { Reducer as weatherReducer } from './component/weather';
			import ReactDOM from 'react-dom';
			import React from 'react';
			import { Provider } from 'react-redux';
			import { View as Weather } from './component/weather';
			import reduxThuck from 'redux-thunk';
			const reducer = combineReducers({
			    weather: weatherReducer,
			});
			
			const initState = {
			    weather: null
			}
			
			let store = createStore(reducer, initState, applyMiddleware(reduxThuck));
			
			ReactDOM.render(
			    <Provider store={store}>
			        <Weather />
			    </Provider>,
			    document.getElementById('root')
			)

##### 8.使用redux-thunk执行异步请求
1. redux-thunk的原理是让action creator支持返回一个方法，方法中可以做异步请求，当请求结束，再次dispatch一个action。
1. 安装redux-thunk：`npm install --save redux-thunk`。
2. 引入thunk并传入applyMiddleware参数中。
3. 在action.js文件中，可以将函数作为action的return。
4. 在获取到api的响应之后，再派发一个update的action，用于实现真正的weather数据更新。

		export const fetchWeather = (city) => {
		    return dispatch => {
		        let url = 'https://www.sojson.com/open/api/weather/json.shtml?city=' + city;
		        dispatch(updateWeather(null));
		        axios.get(url).then(result => {
		            dispatch(updateWeather(result.data));
		        })
		    }
		}

##### 9. 使用redux-saga执行异步请求
1. redux-saga的原理是类似开启一个线程，监听异步action，然后执行分离出来的异步代码，这种方式更易于阅读和测试。
2. 安装redux-saga: `npm install redux-saga --save`。
3. 引入saga: `import  createSagaMiddleware  from  'redux-saga', 
4. 创建saga middleware: `const  sagaMiddleware  =  createSagaMiddleware()`。
5. 



<!--stackedit_data:
eyJoaXN0b3J5IjpbMzgxOTM2OTExLC0xOTc2MjAwNjgxLDE2MT
k1NDEzNDNdfQ==
-->