# SI_2024_lab2_213065

Надица Колоска 213065

![SI_Lab2_213065 drawio (2)](https://github.com/nadd17/SI_2024_lab2_213065/assets/93904427/7e954c0f-800f-423e-9ae7-c22c555fde16)

*Во прилог се обележаните nodes: 
public class SILab2 {
    public static boolean checkCart(List<Item> allItems, int payment){ //1
        
        if (allItems == null){ //2
            throw new RuntimeException("allItems list can't be null!");
        }

        float sum = 0; //3

        for (int i = 0; i < allItems.size(); i++){ // 4 (4.1; 4.2; 4.3)
            Item item = allItems.get(i); //5
            if (item.getName() == null || item.getName().length() == 0){ //6
                item.setName("unknown"); //7
            }
            if (item.getBarcode() != null){ //8
                String allowed = "0123456789"; //9
                char chars[] = item.getBarcode().toCharArray();
                for (int j = 0; j < item.getBarcode().length(); j++){ //10.1 10.2 10.3
                    char c = item.getBarcode().charAt(j); //11
                    if (allowed.indexOf(c) == -1){//12
                        throw new RuntimeException("Invalid character in item barcode!"); //13
                    }
                }
                if (item.getDiscount() > 0){ //14
                    sum += item.getPrice()*item.getDiscount(); //15
                }
                else { /
                    sum += item.getPrice(); //16
                }
            } //17
            else {
                throw new RuntimeException("No barcode!"); //18
            }
            if (item.getPrice() > 300 && item.getDiscount() > 0 && item.getBarcode().charAt(0) == '0'){ //19
                sum -= 30; //20
            }
        }

        if (sum <= payment){ //21
            return true; //22
        }

        else {
            return false; //23
        }
    }
    //24
}

------------------------------------------
CYC = E – N + 2P CYC =  36 - 28 + 2*1 = 10
Цикломатската комплексност на овој код е 10 и таа се добива користејќи ја наведената формула.
Е -  означува број на рабовите кои ги поврзуваат јазлите или таканаречени трансфери на контрола
N - број на јазли во графот или секвенцијална група на изјави кои содржат само еден трансфер на контрола
P -  означува број делови од графот кои се исклучуваат

-----------------------------------
Branch 1: if (allItems == null)

Branch 2: if (item.getName() == null || item.getName().length() == 0)

Branch 3: if (item.getBarcode() != null)

Branch 4: if (allowed.indexOf(c) == -1)

Branch 5: if (item.getDiscount() > 0)

Branch 6: if (item.getPrice() > 300 && item.getDiscount() > 0 && item.getBarcode().charAt(0) == '0')

Branch 7: if (sum <= payment)

1: Покрива случај каде што allItems == null.
input: checkCart (null, 1)

output: RuntimeException

2: Покрива случај каде што името е null, кога има discount и кога payment е поголем од сумата.
input: checkCart ( [(null, "123456", 100, 0.1)], 100)

output: true

3: Покриваат случај каде што нема бар код.
input: checkCart ( [("ImeItem", null, 100, 0.1)], 100)

output: "No barcode"

4:Покриваат случај каде што има невалиден карактер во бар кодот.
input: checkCart ( [("ImeItem", "123456N", 100, 0.1)], 100)

output: "Invalid character in item barcode"

5:Покриваат случај каде што сумата е поголема од payment и каде што нема discount.
input: checkCart ( [("ImeItem", "123456", 1000, 0)], 100)

output: false

6:Покриваат случај каде што се покрива специјалниот попуст.
input: checkCart ( [(null, "0123456", 350, 0.1)], 100)

output: true

-------------------------------------------
