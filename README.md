# EnumsCodable DONE

func enumDecode<T:Codable>(from decoder: Decoder, defaultValue: T) -> T {    
    var result = defaultValue    
    do {
        let key = try decoder.singleValueContainer().decode(T.self)
        result = key
    } catch {
    }    
    return result
}

public enum Enumy: String, Codable {
    case one
    case two
    case wrongValue
    case wrongType
    public init(from decoder: Decoder) throws {
        guard let enumy = Enumy(rawValue: enumDecode(from: decoder, defaultValue: Enumy.wrongType.rawValue)) else {
            self = .wrongType
            return
        }        
        self = enumy
    }
   }
