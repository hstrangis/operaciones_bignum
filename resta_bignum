bignum operator-(const bignum& a, const bignum& b)
{  
    bignum c; // c.digits = {0};
    int dim_c;

    unsigned short *aux;
    if(equal_module(b.digits, b.dim, a.digits, a.dim))
    {    
        if(!(b.sign ^ a.sign)){ 
            c.digits = new unsigned short[1]();
            c.digits[0]=0;
            c.dim=1;
            return c; // XNOR: a = b = true o a = b = false --> c = 0
        }
        c = a + a;
        if(b.sign)
            return c;     // b < 0 y a = b --> c = a + a
        c.sign = NEG;           // a < 0 y a = b --> c = -(a + a)
        return c; 
    }
    if(a.sign && !b.sign)        // a < 0 y b > 0 --> c = -(a + b) 
    {
        bignum aa(a);
        aa.sign = POS;
        c = aa + b;
        c.sign = NEG;
        return c;
    }
    if(!a.sign && b.sign)        // a > 0 y b < 0 --> c = a + b 
    {
        bignum bb(b);
        bb.sign = POS;
        c = a + bb;
        return c;      
    }
    if(bigger(b.digits, b.dim, a.digits, a.dim)) //  b > a --> c = -(b - a) 
    {
        aux = substract(b.digits, b.dim, a.digits, a.dim, dim_c);
        c.digits = new unsigned short[dim_c];
        c.dim = dim_c;
        if(!a.sign)                           // b > a, a > 0 y b > 0 --> c < 0          
            c.sign = NEG;
        copy_array(c.digits, aux, dim_c);
        delete []aux;
        return c;
    }                                                       // a > b --> c = a - b                        
    aux = substract(a.digits, a.dim, b.digits, b.dim, dim_c);
    c.digits = new unsigned short[dim_c];
    c.dim = dim_c;
    if(a.sign)                  // a > b, a < 0 y b < 0 --> c < 0
        c.sign = NEG;
    copy_array(c.digits, aux, dim_c);
    delete []aux;
    return c;
}

unsigned short *substract(unsigned short *a, int na, unsigned short *b, int nb, int &nc)
{
    unsigned short *c = new unsigned short[na]();
    nc = na;

    for(int i = 0; i < nb; i++)
    {
        if(a[i] < b[i])             //Pide carry   
        {
            a[i] += 10; 
            c[i] = a[i] - b[i];
            if(a[i + 1] != 0)       //Si el que sigue no es zero le resta 1
                a[i + 1]--;
            else                    //Si es zero, sigue hasta encontrar un num > 0
            {
                int j = i + 1;
                while(a[j] == 0)
                {    
                    a[j] = 9;
                    j++;
                }
                a[j]--;
            }    
        }
        else if(a[i] > b[i])
            c[i] = a[i] - b[i];
        else c[i] = 0;        
    }
    for(int i = nb; i < na; i++)    //Completa los restantes
        c[i] = a[i];
    
    if(c[na - 1] == 0)              //Si cambia la dimension de la resta, la ajusta   
        nc = resize(c, na);
    return c; 
}
