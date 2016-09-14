# DivideTwoNumbers
divides two numbers and the delegate class prints passed error if function throws
//
//  ViewController.swift
//  bluejay
//
//  Created by Peter Cupples on 9/10/16.
//  Copyright © 2016 Peter Cupples. All rights reserved.
//

import Cocoa

protocol CookieBatch {
    func errorDidOccur(_: ErrorType)
}

class ViewController: NSViewController {
    @IBOutlet weak var numerator: NSTextField!
    @IBOutlet weak var denominator: NSTextField!
    @IBOutlet weak var button: NSButton!
    @IBOutlet weak var ratioDisplay: NSTextField!
    
    var num1: Double?
    var num2: Double?
    var delegate: CookieBatch
    var cashCab: ErrorType?
    var ratio = 0.0
    
    required init?(coder: NSCoder) {
        self.delegate = BAM()
        super.init(coder:coder)
    }
    
    
    @IBAction func handleClick(sender: NSButton) {
        num1 = Double(numerator.stringValue)
        num2 = Double(denominator.stringValue)
        do { ratio = try divide(num1, b: num2)
            ratioDisplay.stringValue = "\(ratio)"
        } catch { cashCab = error
            delegate.errorDidOccur(cashCab!) }
    }
    
    func divide(a: Double?, b: Double?) throws -> Double {
        guard let a = a, let b = b where a >= 0.0 || a <= 0.0 && b > 0.0 || b < 0.0
            else { throw NSError(domain: NSURLErrorDomain, code: NSURLErrorCannotOpenFile, userInfo:nil)}
        return a / b
    }
    
    override func viewDidLoad() {
        numerator.stringValue = "0"
        denominator.stringValue = "0"
        super.viewDidLoad()
        
        // Do any additional setup after loading the view.
    }
}
class BAM: NSObject, CookieBatch {
    var cashCab: ErrorType?
    func errorDidOccur(_: ErrorType) {
        print("Either a or b is not a number, or b is equal to zero. Error: \(cashCab)")
    }
}

