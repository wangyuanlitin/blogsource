---
title: react-router V4.3.1
date: 2018-09-13 14:24:06
tags: JavaScript
---

------

**Part01. Switch.js**

``` javascript
// 部分代码
render() {
  const { route } = this.context.router;
  const { children } = this.props;
  const location = this.props.location || route.location;
  
  let match, child;
  React.Children.forEach(children, element => {
    // match不为空时跳过
    if (match == null && React.isValidElement(element)) {
      const {
        path: pathProp,
        exact,
        strict,
        sensitive,
        from
      } = element.props;
      const path = pathProp || from;

      child = element;
      match = matchPath( // 生成出来的是什么？
        location.pathname,
        { path, exact, strict, sensitive },
        route.match
      );
    }
  });

  return match
    ? React.cloneElement(child, { location, computedMatch: match })
    : null;
}
```
<!--more-->
使用Switch包裹Route时，路由只会匹配一个

实现路由应该只是dom element的切换，并不是通过pushState和replaceState实现的

**Part02. Route.js**

```javascript
render() {
  const { match } = this.state;
  const { children, component, render } = this.props;
  const { history, route, staticContext } = this.context.router;
  const location = this.props.location || route.location;
  const props = { match, location, history, staticContext };

  if (component) return match ? React.createElement(component, props) : null; // createElement props 里面的history做了什么

  if (render) return match ? render(props) : null;

  if (typeof children === "function") return children(props);

  if (children && !isEmptyChildren(children))
    return React.Children.only(children);

  return null;
}
```
四种情况，都是createElement, render, children 生成的，也是通过这种方式切换的路由

**Part03. Redirect.js**
```javascript
isStatic() {
  return this.context.router && this.context.router.staticContext;
}
perform() {
  const { history } = this.context.router;
  const { push } = this.props;
  const to = this.computeTo(this.props);

  if (push) {
    history.push(to);
  } else {
    history.replace(to);
  }
}
```

这个是通过push，replace实现的，应该是React自带的push，replace

**Part04 Router.js**
```javascript
render() {
  const { children } = this.props;
  return children ? React.Children.only(children) : null;
}
```
应该就是包了一下Route吧，没有实际作用，可能需要看一下React.Children.only做了什么

Part05 withRouter.js

```javascript
const withRouter = Component => {
  const C = props => {
    const { wrappedComponentRef, ...remainingProps } = props;
    return (
      <Route
        children={routeComponentProps => (
          <Component
            {...remainingProps}
            {...routeComponentProps}
            ref={wrappedComponentRef}
          />
        )}
      />
    );
  };

  C.displayName = `withRouter(${Component.displayName || Component.name})`;
  C.WrappedComponent = Component;
  C.propTypes = {
    wrappedComponentRef: PropTypes.func
  };

  return hoistStatics(C, Component);
};

export default withRouter;
```
用Route wrapper component 注入history参数