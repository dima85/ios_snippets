```drawRect``` - called after bound already set 


### Shadow border for view
 ```       
btnCreateOffer.layer.shadowColor = UIColor.grayColor().CGColor
btnCreateOffer.layer.shadowOpacity = 1
btnCreateOffer.layer.shadowOffset = CGSizeZero
btnCreateOffer.layer.shadowRadius = 3
btnCreateOffer.layer.cornerRadius = 3
```

### NSAttributedString Text with image in front of text
```
let noRistkImage = NSTextAttachment()
noRistkImage.image = UIImage(hhvNamed: "info_positive")
noRistkImage.bounds = CGRect(origin: CGPointZero, size: CGSize(width: 12, height: 10))

let noRiskTextImage = NSAttributedString(attachment: noRistkImage)

var text = NSMutableAttributedString(attributedString: noRiskTextImage)


var noRiskTextValue = NSAttributedString(string: " Kein Risiko: Vertrag ist 14 Tage widerrufbar!", attributes: [NSForegroundColorAttributeName : HHVColors.greenNoRiskColor])

text.appendAttributedString(noRiskTextValue)
 
```

### Calculate size/height of multiline label
```
extension UILabel {
    
    static func requiredSize(width:CGFloat, text:String, font:UIFont) -> CGSize{
        
        let label:UILabel = UILabel(frame: CGRectMake(0, 0, width, CGFloat.max))
        label.numberOfLines = 0
        label.lineBreakMode = NSLineBreakMode.ByWordWrapping
        label.font = font
        label.text = text
        
        label.sizeToFit()
        
        return label.frame.size
    }
    
    static func requiredWidth(text:String, font:UIFont) -> CGFloat {
        return requiredSize(10000, text:text, font:font).width
    }
    
    static func requiredHeight(width:CGFloat, text:String, font:UIFont) -> CGFloat {
        return requiredSize(width, text:text, font:font).height
    }
    
    static func requiredHeight(width:CGFloat, attributedText:NSAttributedString, font:UIFont) -> CGFloat{
        
        let label:UILabel = UILabel(frame: CGRectMake(0, 0, width, 0))
        label.numberOfLines = 0
        label.lineBreakMode = NSLineBreakMode.ByWordWrapping
        label.font = font
        label.attributedText = attributedText
        label.sizeToFit()
        let height = label.frame.height
        return height
    }
}
 ```
