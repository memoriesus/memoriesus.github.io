---
layout: post
title: RxSwift双向绑定
tags: [iOS Programming, best practices,RxSwift]
readtime: true
comment: true
---

# 

在这种情况下，双向绑定不会导致无限循环，因为UI元素在以编程方式进行修改时不会发出值，而是仅在用户更改值时才执行此操作。如果用户按下开关，它将被推到Subject [BehaviorRelay]，然后，该主题将值推回到开关，但到此为止。）

您将必须将Element强制转换为Any？与地图和地图的任何？从BehaviorRelay转到UI元素时，返回到正确的类型。这样做非常笨拙且不安全。

最好将BehaviorRelay的元素设置为正确的类型。无论如何，您将必须知道类型，以便对其进行任何有用的处理。


目前我想知道如何在RxSwift imaging have一个具有可变属性的ViewModel中进行双向绑定。这些是RxSwfit为它们之间的单向数据绑定提供了以下方法。viewModel。文本。绑定（到：标签。接收。文本）。使用RxBinding中的~>（bind（to:））和~（disposed（by:））运算符来处理（by:disposeBag），我们可以用下面的简单代码进行绑定。

一种在UIControl上实现双向绑定的方法，如SwiftBond，或成熟的反应库，如RxSwift、RxCocoa。双向绑定本质上是双向设置中的观察者侦听器（或Pub/Sub）模式。这两个参与者（通常是一个控件和一个DataProvider）相互绑定，以便在值发生更改时，相应组件的侦听器将收到值更改的通知。
但有时我们需要实现双向绑定。

`

import UIKit
import RxSwift
import RxCocoa

class UserViewModel {
    let username = BehaviorSubject<String?>(value: "")
}


class ViewController: UIViewController {

    @IBOutlet weak var email: UITextField!

    var userViewModel = UserViewModel()
    let bag = DisposeBag()

    override func viewDidLoad() {
        super.viewDidLoad()

        userViewModel.username.asObservable().subscribe { print($0) }.disposed(by: bag)
        (email.rx.text <-> userViewModel.username).disposed(by: bag)

        // clear value of the username.
        DispatchQueue.main.asyncAfter(deadline: .now()+5) {
            self.userViewModel.username.onNext(nil)
        }
    }
}

infix operator <->

@discardableResult func <-><T>(property: ControlProperty<T>, variable: BehaviorSubject<T>) -> Disposable {
    let variableToProperty = variable.asObservable()
        .bind(to: property)

    let propertyToVariable = property
        .subscribe(
            onNext: { variable.onNext($0) },
            onCompleted: { variableToProperty.dispose() }
    )

    return Disposables.create(variableToProperty, propertyToVariable)
}`


