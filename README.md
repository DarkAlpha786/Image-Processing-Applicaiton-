# Image-Processing-Applicaiton-
Using SWIFT-5 to creating fully functioning Image processing application for iPhones

//
//  ViewController.swift
//  Filterer1
//
//  Created by Mustafa Poonawala on 9/7/18.
//  Copyright © 2018 Mustafa Poonawala. All rights reserved.
//

import UIKit

class ViewController: UIViewController, UIImagePickerControllerDelegate, UINavigationControllerDelegate {
	
	let shapeLayer = CAShapeLayer()
	let tracklayer = CAShapeLayer()
	let label = UILabel()
	
	var RedFilterImg: UIImage?
	var GreenFilterImg: UIImage?
	var BlueFilterImg: UIImage?
	var YellowFilterImg: UIImage?
	var PurpleFilterImg: UIImage?

	@IBOutlet var imageView: UIImageView!
	@IBOutlet var redImageViewPreview: UIImageView!
	@IBOutlet var greenImageViewPreview: UIImageView!
	@IBOutlet var blueImageViewPreview: UIImageView!
	@IBOutlet var yellowImageViewPreview: UIImageView!
	@IBOutlet var purpleImageViewPreview: UIImageView!
	
	@IBOutlet var Filter: UIButton!
	@IBOutlet var compare: UIButton!
	
	@IBOutlet var redFilter: UIButton!
	@IBAction func onRedFilter(sender: UIButton) {
		if (redFilter.selected){
			loadingStatusExit()
			redFilter.selected = false
		}else {
			loadingStatusEntryR()
			redFilter.selected = true
		}
	}
	
	@IBOutlet var greenFilter: UIButton!
	@IBAction func onGreenFilter(sender: UIButton) {
		if (greenFilter.selected){
			loadingStatusExit()
			greenFilter.selected = false
		}else {
			loadingStatusEntryG()
			greenFilter.selected = true
		}
	}
	
	@IBOutlet var blueFilter: UIButton!
	@IBAction func onBlueFilter(sender: UIButton) {
		if (blueFilter.selected){
			loadingStatusExit()
			blueFilter.selected = false
		}else {
			loadingStatusEntryB()
			blueFilter.selected = true
		}
	}
	
	@IBOutlet var yellowFilter: UIButton!
	@IBAction func onYellowFilter(sender: UIButton) {
		if (yellowFilter.selected){
			loadingStatusExit()
			yellowFilter.selected = false
		}else {
			loadingStatusEntryY()
			yellowFilter.selected = true
		}
		
	}
	
	@IBOutlet var purpleFilter: UIButton!
	@IBAction func onPurpleFilter(sender: UIButton) {
		if (purpleFilter.selected){
			loadingStatusExit()
			purpleFilter.selected = false
		}else {
			loadingStatusEntryP()
			purpleFilter.selected = true
		}
	}

	@IBOutlet var newPhoto: UIButton!
	
	@IBOutlet var secondaryMenu: UIView!
	@IBOutlet var bottomMenu: UIView!
	
	override func viewDidLoad() {
		super.viewDidLoad()
		secondaryMenu.backgroundColor = UIColor.whiteColor().colorWithAlphaComponent(0.5)
		secondaryMenu.translatesAutoresizingMaskIntoConstraints = false
		
		compare.enabled = false
		
		Red()
		Green()
		Blue()
		Yellow()
		Purple()
		
	}
	
	override func preferredStatusBarStyle() -> UIStatusBarStyle {
		return UIStatusBarStyle.LightContent
	}

	override func didReceiveMemoryWarning() {
		super.didReceiveMemoryWarning()
		// Dispose of any resources that can be recreated.
	}
	
	func Red(){
		let image1 = UIImage(named: "sample2")!
		var myRGBA1 = RGBAImage(image : image1)!
		let avgRed = 67
		
		for y in 0..<myRGBA1.height{
			for x in 0..<myRGBA1.width{
				let index = y * myRGBA1.width + x
				var pixel = myRGBA1.pixels[index]
				let redDelta = Int(pixel.red) - avgRed
				var modifier = 1 + 4 * (Double(y) / Double(myRGBA1.height))
				if (Int(pixel.red) < avgRed) {
					modifier = 1
				}
				
				pixel.red = UInt8(max(min(255, Int(round(Double(avgRed) + modifier * Double(redDelta)))), 0))
				myRGBA1.pixels[index] = pixel
				
			}
		}
		RedFilterImg = myRGBA1.toUIImage()
	}

	func Green(){
		let image1 = UIImage(named: "sample2")!
		var myRGBA1 = RGBAImage(image : image1)!
		let avgGreen = 98
		
		for y in 0..<myRGBA1.height{
			for x in 0..<myRGBA1.width{
				let index = y * myRGBA1.width + x
				var pixel = myRGBA1.pixels[index]
				let greenDelta = Int(pixel.green) - avgGreen
				var modifier = 1 + 4 * (Double(y) / Double(myRGBA1.height))
				if (Int(pixel.green) < avgGreen) {
					modifier = 1
				}
				
				pixel.green = UInt8(max(min(255, Int(round(Double(avgGreen) + modifier * Double(greenDelta)))), 0))
				myRGBA1.pixels[index] = pixel
				
			}
		}
		GreenFilterImg = myRGBA1.toUIImage()
	}
	
	func Blue(){
		let image1 = UIImage(named: "sample2")!
		var myRGBA1 = RGBAImage(image : image1)!
		let avgblue = 83
		
		for y in 0..<myRGBA1.height{
			for x in 0..<myRGBA1.width{
				let index = y * myRGBA1.width + x
				var pixel = myRGBA1.pixels[index]
				let blueDelta = Int(pixel.blue) - avgblue
				var modifier = 1 + 4 * (Double(y) / Double(myRGBA1.height))
				if (Int(pixel.blue) < avgblue) {
					modifier = 1
				}
				
				pixel.blue = UInt8(max(min(255, Int(round(Double(avgblue) + modifier * Double(blueDelta)))), 0))
				myRGBA1.pixels[index] = pixel
				
			}
		}
		BlueFilterImg = myRGBA1.toUIImage()
	}
	
	func Yellow(){
		let image1 = UIImage(named: "sample2")!
		var myRGBA1 = RGBAImage(image : image1)!
		let avgRed = 67
		let avgGreen = 98
		
		
		for y in 0..<myRGBA1.height{
			for x in 0..<myRGBA1.width{
				let index = y * myRGBA1.width + x
				var pixel = myRGBA1.pixels[index]
				let redDelta = Int(pixel.red) - avgRed
				let greenDelta = Int(pixel.green) - avgGreen
				var modifier = 1 + 4 * (Double(y) / Double(myRGBA1.height))
				if (Int(pixel.red) < avgRed) {
					modifier = 1
				}
				
				pixel.red = UInt8(max(min(255, Int(round(Double(avgRed) + modifier * Double(redDelta)))), 0))
				pixel.green = UInt8(max(min(255, Int(round(Double(avgGreen) + modifier * Double(greenDelta)))), 0))
				myRGBA1.pixels[index] = pixel
				
			}
		}
		YellowFilterImg = myRGBA1.toUIImage()
	}
	
	func Purple(){
		let image1 = UIImage(named: "sample2")!
		var myRGBA1 = RGBAImage(image : image1)!
		let avgblue = 118
		let avgRed  = 50
		
		for y in 0..<myRGBA1.height{
			for x in 0..<myRGBA1.width{
				let index = y * myRGBA1.width + x
				var pixel = myRGBA1.pixels[index]
				let blueDelta = Int(pixel.blue) - avgblue
				var modifier = 1 + 4 * (Double(y) / Double(myRGBA1.height))
				if (Int(pixel.blue) < avgblue) {
					modifier = 1
				}
				let redDelta = Int(pixel.red) - avgRed
				if (Int(pixel.red) < avgRed) {
					modifier = 1
				}
				
				pixel.red = UInt8(max(min(255, Int(round(Double(avgRed) + modifier * Double(redDelta)))), 0))
				
				pixel.blue = UInt8(max(min(255, Int(round(Double(avgblue) + modifier * Double(blueDelta)))), 0))
				myRGBA1.pixels[index] = pixel
				
			}
		}
		PurpleFilterImg = myRGBA1.toUIImage()
	}
	
	@IBAction func onFilters(sender: UIButton) {
		if (sender.selected) {
			hideSecondaryMenu()
			sender.selected = false
		} else {
			showSecondaryMenu()
			sender.selected = true
		}
		redImageViewPreview.image = RedFilterImg
		greenImageViewPreview.image = GreenFilterImg
		blueImageViewPreview.image = BlueFilterImg
		yellowImageViewPreview.image = YellowFilterImg
		purpleImageViewPreview.image = PurpleFilterImg
		
		if (Filter.selected == true) {
			compare.enabled = true
		}else{
			compare.enabled = false
		}

	}
	
	@IBAction func onCompare(sender: UIButton) {
		if (compare.selected){
			if (redFilter.selected == true) {
				imageView.image = RedFilterImg
			}else if(greenFilter.selected == true){
				imageView.image = GreenFilterImg
			}else if(blueFilter.selected == true){
				imageView.image = BlueFilterImg
			}else if(yellowFilter.selected == true){
				imageView.image = YellowFilterImg
			}else if(purpleFilter.selected == true){
				imageView.image = PurpleFilterImg
			}else{
				let image1 = UIImage(named: "sample2")!
				imageView.image = image1
			}
			compare.selected = false
		}else{
			let image1 = UIImage(named: "sample2")!
			imageView.image = image1
			compare.selected = true
		}
		
	}

	@IBAction func onShare(sender: AnyObject) {
		let activityController = UIActivityViewController(activityItems: [imageView.image!], applicationActivities: nil)
		
		presentViewController(activityController, animated: true, completion: nil)
	}
	
	@IBAction func onNewPhotos(sender: UIButton) {
		
		let actionSheet = UIAlertController(title: nil, message: nil, preferredStyle: .ActionSheet)
		
		actionSheet.addAction(UIAlertAction(title: "Camera", style: .Default, handler: { action in
			self.showCamera()
		}))
		
		actionSheet.addAction(UIAlertAction(title: "Album", style: .Default, handler: { action in
			self.showAlbum()
		}))
		
		actionSheet.addAction(UIAlertAction(title: "Cancel", style: .Cancel, handler: nil))
		
		self.presentViewController(actionSheet, animated: true, completion: nil)

	}
	
	func showCamera() {
		let cameraPicker = UIImagePickerController()
		cameraPicker.delegate = self
		cameraPicker.sourceType = .Camera
		
		presentViewController(cameraPicker, animated: true, completion: nil)
	}
	
	func showAlbum() {
		let cameraPicker = UIImagePickerController()
		cameraPicker.delegate = self
		cameraPicker.sourceType = .PhotoLibrary
		
		presentViewController(cameraPicker, animated: true, completion: nil)
	}

	// MARK: UIImagePickerControllerDelegate
	func imagePickerController(picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : AnyObject]) {
		dismissViewControllerAnimated(true, completion: nil)
		if let image = info[UIImagePickerControllerOriginalImage] as? UIImage {
			imageView.image = image
		}
	}
	
	func imagePickerControllerDidCancel(picker: UIImagePickerController) {
		dismissViewControllerAnimated(true, completion: nil)
	}

	func showSecondaryMenu() {
		view.addSubview(secondaryMenu)
		
		let bottomConstraint = secondaryMenu.bottomAnchor.constraintEqualToAnchor(bottomMenu.topAnchor)
		let leftConstraint = secondaryMenu.leftAnchor.constraintEqualToAnchor(view.leftAnchor)
		let rightConstraint = secondaryMenu.rightAnchor.constraintEqualToAnchor(view.rightAnchor)
		
		let heightConstraint = secondaryMenu.heightAnchor.constraintEqualToConstant(120)
		
		NSLayoutConstraint.activateConstraints([bottomConstraint, leftConstraint, rightConstraint, heightConstraint])
		
		view.layoutIfNeeded()
		
		self.secondaryMenu.alpha = 0
		UIView.animateWithDuration(0.4) {
			self.secondaryMenu.alpha = 1.0
		}
	}
	
	func hideSecondaryMenu() {
		UIView.animateWithDuration(0.4, animations: {
			self.secondaryMenu.alpha = 0
		}) { completed in
			if completed == true {
				self.secondaryMenu.removeFromSuperview()
			}
		}
	}
	
	func loadingStatusEntryR(){
		animateCircle()
		creatingCircleAndTracker()
		creatingLabel()
		dimissAndAddingFilteredImageR()
	}
	
	func loadingStatusEntryG(){
		animateCircle()
		creatingCircleAndTracker()
		creatingLabel()
		dimissAndAddingFilteredImageG()
	}
	
	func loadingStatusEntryB(){
		animateCircle()
		creatingCircleAndTracker()
		creatingLabel()
		dimissAndAddingFilteredImageB()
	}
	
	func loadingStatusEntryY(){
		animateCircle()
		creatingCircleAndTracker()
		creatingLabel()
		dimissAndAddingFilteredImageY()
	}
	
	func loadingStatusEntryP(){
		animateCircle()
		creatingCircleAndTracker()
		creatingLabel()
		dimissAndAddingFilteredImageP()
	}
	
	func loadingStatusExit(){
		animateCircle()
		creatingCircleAndTracker()
		creatingLabel()
		dimissAndAddingOriginalImage()
	}
	
	func creatingLabel() {
		let WFAM: UILabel = {
			label.text = "Wait for a moment"
			label.textAlignment = NSTextAlignment.Center
			label.lineBreakMode = .ByWordWrapping
			label.numberOfLines = 2
			label.font = UIFont.boldSystemFontOfSize(25)
			return label
		}()
		view.addSubview(WFAM)
		WFAM.frame = CGRect(x: 0, y: 0, width: 150, height: 100)
		WFAM.center = view.center
	}
	
	func creatingCircleAndTracker(){
		// creating my track layer
		let circularPath = UIBezierPath(arcCenter: .zero, radius: 100, startAngle: 0,endAngle: 2 * 3.14  , clockwise: true)
		tracklayer.path = circularPath.CGPath
		
		tracklayer.strokeColor = UIColor.lightGrayColor().CGColor
		tracklayer.lineWidth = 10
		tracklayer.fillColor = UIColor.clearColor().CGColor
		tracklayer.lineCap = kCALineCapRound
		tracklayer.position = view.center
		view.layer.addSublayer(tracklayer)
		
		//creating my circle
		shapeLayer.path = circularPath.CGPath
		
		shapeLayer.strokeColor = UIColor.redColor().CGColor
		shapeLayer.lineWidth = 10
		shapeLayer.fillColor = UIColor.clearColor().CGColor
		shapeLayer.lineCap = kCALineCapRound
		shapeLayer.position = view.center
		view.layer.addSublayer(shapeLayer)
		
		//Allow to rotate some object on the screen
		shapeLayer.transform = CATransform3DMakeRotation(-3.14/2, 0, 0, 1)
		
		//when use of button this allows to start the red line at 12'oclock
		shapeLayer.strokeEnd = 0

	}
	
	func animateCircle(){
		shapeLayer.strokeEnd = 0
		let CAbasicAnimation = CABasicAnimation(keyPath: "strokeEnd")
		CAbasicAnimation.toValue = 1
		CAbasicAnimation.duration = 0.75
		
		CAbasicAnimation.fillMode = kCAFillModeForwards
		CAbasicAnimation.removedOnCompletion = false
		
		shapeLayer.addAnimation(CAbasicAnimation, forKey: "strokeEnd")
	}
	
	func dimissAndAddingFilteredImageR() {
		label.alpha = 1
		UIView.animateWithDuration(1, animations: {
			self.label.alpha = 0
		}) { (true) in
			UIView.animateWithDuration(1, animations: {
				self.shapeLayer.strokeColor = UIColor.clearColor().CGColor
				}, completion: {(true) in
					UIView.animateWithDuration(1, animations: {
						self.tracklayer.strokeColor = UIColor.clearColor().CGColor
						}, completion: { (true) in
							UIView.animateWithDuration(0.25, delay: 0.5, options: [], animations: {
								self.imageView.image = self.RedFilterImg
								}, completion: nil)
					})
			})
			
		}
		
	}

	func dimissAndAddingFilteredImageG() {
		label.alpha = 1
		UIView.animateWithDuration(1, animations: {
			self.label.alpha = 0
		}) { (true) in
			UIView.animateWithDuration(1, animations: {
				self.shapeLayer.strokeColor = UIColor.clearColor().CGColor
				}, completion: {(true) in
					UIView.animateWithDuration(1, animations: {
						self.tracklayer.strokeColor = UIColor.clearColor().CGColor
						}, completion: { (true) in
							UIView.animateWithDuration(0.25, delay: 0.5, options: [], animations: {
								//self.imageView.alpha = 1
								self.imageView.image = self.GreenFilterImg
								}, completion: nil)
					})
			})
			
		}
		
	}
	
	func dimissAndAddingFilteredImageB() {
		label.alpha = 1
		UIView.animateWithDuration(1, animations: {
			self.label.alpha = 0
		}) { (true) in
			UIView.animateWithDuration(1, animations: {
				self.shapeLayer.strokeColor = UIColor.clearColor().CGColor
				}, completion: {(true) in
					UIView.animateWithDuration(1, animations: {
						self.tracklayer.strokeColor = UIColor.clearColor().CGColor
						}, completion: { (true) in
							UIView.animateWithDuration(0.25, delay: 0.5, options: [], animations: {
								//self.imageView.alpha = 1
								self.imageView.image = self.BlueFilterImg
								}, completion: nil)
					})
			})
			
		}
		
	}
	
	func dimissAndAddingFilteredImageY() {
		label.alpha = 1
		UIView.animateWithDuration(1, animations: {
			self.label.alpha = 0
		}) { (true) in
			UIView.animateWithDuration(1, animations: {
				self.shapeLayer.strokeColor = UIColor.clearColor().CGColor
				}, completion: {(true) in
					UIView.animateWithDuration(1, animations: {
						self.tracklayer.strokeColor = UIColor.clearColor().CGColor
						}, completion: { (true) in
							UIView.animateWithDuration(0.25, delay: 0.5, options: [], animations: {
								//self.imageView.alpha = 1
								self.imageView.image = self.YellowFilterImg
								}, completion: nil)
					})
			})
			
		}
		
	}
	
	func dimissAndAddingFilteredImageP() {
		label.alpha = 1
		UIView.animateWithDuration(1, animations: {
			self.label.alpha = 0
		}) { (true) in
			UIView.animateWithDuration(1, animations: {
				self.shapeLayer.strokeColor = UIColor.clearColor().CGColor
				}, completion: {(true) in
					UIView.animateWithDuration(1, animations: {
						self.tracklayer.strokeColor = UIColor.clearColor().CGColor
						}, completion: { (true) in
							UIView.animateWithDuration(0.25, delay: 0.5, options: [], animations: {
								//self.imageView.alpha = 1
								self.imageView.image = self.PurpleFilterImg
								}, completion: nil)
					})
			})
			
		}
		
	}
	
	func dimissAndAddingOriginalImage() {
		let image1 = UIImage(named: "sample2")!
		label.alpha = 1
		UIView.animateWithDuration(1, animations: {
			self.label.alpha = 0
		}) { (true) in
			UIView.animateWithDuration(1, animations: {
				self.shapeLayer.strokeColor = UIColor.clearColor().CGColor
				}, completion: {(true) in
					UIView.animateWithDuration(1, animations: {
						self.tracklayer.strokeColor = UIColor.clearColor().CGColor
						}, completion: { (true) in
							UIView.animateWithDuration(0.25, delay: 0.5, options: [], animations: {
								self.imageView.image = image1
								}, completion: nil)
					})
			})
			
		}
	}
}


