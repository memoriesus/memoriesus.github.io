---
post: page
title: change dark mode on iOS
tags: [iOS]
comment: true
---

Change the window UserInterfaceStyle for iOS 13+ version. Just set:
`UIApplication.shared.changeStatusBarStyle(.light)
`
or
`UIApplication.shared.changeStatusBarStyle(.dark)`


Give UIApplication one method to do it like that:
`extension UIApplication {
	enum StatusColor {
		case dark,light
		}
		public func changeStatusBarStyle(_ mode:StatusColor = .light) {
			if #available(iOS 13.0,*) {
				guard let appDelegate = delegate as? AppDelegate else {
					return}
					var interfaceStyle:UIUserInterfaceStyle
					switch mode {
						case .dark:
						interfaceStyle = .dark
						default:
						interfaceStyle = .light
						}
						appDelegate.window?.overrideUseInterfaceStyle = interfaceStyle}
						}
						}`



