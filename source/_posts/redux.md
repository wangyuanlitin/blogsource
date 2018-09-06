---
title: React 使用 Redux
date: 2018-09-06 16:05:21
tags: 前端
---

------

用了这么久前端了，一直没搞懂redux怎么用，最近这两天看了redux官网examples, 动手写了cnode的例子，只实现了获取切换tab获取数据功能


之前不懂怎么初始化数据，还有view调用action后，action怎么通过dispatch让reducer去更改state


##### 1. 初始化数据还是在react的生命周期内触发action
##### 2. action 和 reducer 主要在connect的时候，通过mapDispatchToProps建立联系，action获取数据后，dispatch一个信号，reducer接收到后更新state
##### 3. reducer更新完state后，数据流自上而下更新，组件内通过connect mapStateToProps 获取相应state的值

<!--more-->

```javascript
// Topics.jsx 容器组件
import { loadTopics } from '../actions/actionTypes'

class Topics extends React.Component {
  // 生命周期内触发action
  componentDidMount() {
    this.props.loadTopics('all') // 初始获取所有的topics
  }
  render() {
    const { topics } = this.props
  }
}

Topics.propTypes = {
  loadTopics: PropTypes.func.isRequired
}

// state.topics更新后，相应的render也更新
const mapStateToProps = (state) => {
  return {
    topics: state.topics
  }
}

export default connect(mapStateToProps, { loadTopics })(Topics)


// actionTypes
export const FETCH_TOPICS_LIST = 'FETCH_TOPICS_LIST'

export function loadTopics (tab) {
  return async (dispatch) => {
    let res = await fetch(`https://cnodejs.org/api/v1/topics?tab=${tab}`)
    res = await res.json() // 请求完成后，通过dispatch更新state
    dispatch({
      type: FETCH_TOPICS_LIST,
      topics: res.data
    })
  }
}

// reducer
import { FETCH_TOPICS_LIST } from '../actions/actionTypes'

const topics = (state = {}, action) => {
  switch(action.type) {
    case FETCH_TOPICS_LIST:
      // 更新topics
      return {
        topics: action.topics
      }
    default:
      return state
  }
}

export default topics
```

占坑，后续补一下mapDispatchToProps的内容，不懂dispatch是怎么传进去的