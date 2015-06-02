# Polynomials

package poly;

import java.io.*;
import java.util.StringTokenizer;

/**
 * This class implements a term of a polynomial.
 * 
 * @author runb-cs112
 *
 */
class Term {
	/**
	 * Coefficient of term.
	 */
	public float coeff;
	
	/**
	 * Degree of term.
	 */
	public int degree;
	
	/**
	 * Initializes an instance with given coefficient and degree.
	 * 
	 * @param coeff Coefficient
	 * @param degree Degree
	 */
	public Term(float coeff, int degree) {
		this.coeff = coeff;
		this.degree = degree;
	}
	
	/* (non-Javadoc)
	 * @see java.lang.Object#equals(java.lang.Object)
	 */
	public boolean equals(Object other) {
		return other != null &&
		other instanceof Term &&
		coeff == ((Term)other).coeff &&
		degree == ((Term)other).degree;
	}
	
	/* (non-Javadoc)
	 * @see java.lang.Object#toString()
	 */
	public String toString() {
		if (degree == 0) {
			return coeff + "";
		} else if (degree == 1) {
			return coeff + "x";
		} else {
			return coeff + "x^" + degree;
		}
	}
}

/**
 * This class implements a linked list node that contains a Term instance.
 * 
 * @author runb-cs112
 *
 */
class Node {
	
	/**
	 * Term instance. 
	 */
	Term term;
	
	/**
	 * Next node in linked list. 
	 */
	Node next;
	
	/**
	 * Initializes this node with a term with given coefficient and degree,
	 * pointing to the given next node.
	 * 
	 * @param coeff Coefficient of term
	 * @param degree Degree of term
	 * @param next Next node
	 */
	public Node(float coeff, int degree, Node next) {
		term = new Term(coeff, degree);
		this.next = next;
	}
}

/**
 * This class implements a polynomial.
 * 
 * @author runb-cs112
 *
 */
public class Polynomial {
	
	/**
	 * Pointer to the front of the linked list that stores the polynomial. 
	 */ 
	Node poly;
	
	/** 
	 * Initializes this polynomial to empty, i.e. there are no terms.
	 *
	 */
	public Polynomial() {
		poly = null;
	}
	
	/**
	 * Reads a polynomial from an input stream (file or keyboard). The storage format
	 * of the polynomial is:
	 * <pre>
	 *     <coeff> <degree>
	 *     <coeff> <degree>
	 *     ...
	 *     <coeff> <degree>
	 * </pre>
	 * with the guarantee that degrees will be in descending order. For example:
	 * <pre>
	 *      4 5
	 *     -2 3
	 *      2 1
	 *      3 0
	 * </pre>
	 * which represents the polynomial:
	 * <pre>
	 *      4*x^5 - 2*x^3 + 2*x + 3 
	 * </pre>
	 * 
	 * @param br BufferedReader from which a polynomial is to be read
	 * @throws IOException If there is any input error in reading the polynomial
	 */
	public Polynomial(BufferedReader br) throws IOException {
		String line;
		StringTokenizer tokenizer;
		float coeff;
		int degree;
		
		poly = null;
		
		while ((line = br.readLine()) != null) {
			tokenizer = new StringTokenizer(line);
			coeff = Float.parseFloat(tokenizer.nextToken());
			degree = Integer.parseInt(tokenizer.nextToken());
			poly = new Node(coeff, degree, poly);
		}
	}
	
	
	/**
	 * Returns the polynomial obtained by adding the given polynomial p
	 * to this polynomial - DOES NOT change this polynomial
	 * 
	 * @param p Polynomial to be added
	 * @return A new polynomial which is the sum of this polynomial and p.
	 */
	public Polynomial add(Polynomial p) {
		if(this.poly==null)

			return p;

		if(p.poly==null)

			return this;

		Node tmp=this.poly;

		Node tmp2=p.poly;
		
		Node insert=null;
		
		
	



		while(tmp2!=null){

			
			if(tmp==null){
			
			insert = tmp2;
			
			insert(insert);
			
			
			
			
			

			
			tmp2=tmp2.next;
			
			

			tmp=poly;

		}





			else if(tmp.term.degree==tmp2.term.degree){
				
			tmp.term.coeff=tmp.term.coeff+tmp2.term.coeff;

			
			tmp2=tmp2.next;

			tmp=poly;

		}

			else{

			tmp=tmp.next;

		}

	}
			if(allZeros(poly)==true)
				return null;
			return deleteAllZeros(this, 0);
			
	}
	
	
	
	
	private void insert(Node thing){
		
		Node cast=new Node(thing.term.coeff,thing.term.degree,thing.next);
		Node current=this.poly, previous=null;
		
		if(current==null){
			cast.next=null;
			poly=cast;
			return;
		}

		while(current != null){

		if(thing.term.degree < current.term.degree && current.equals(this.poly)){

			
		cast.next=current;

		poly=cast;
		current=current.next;
		
		return;
		
		

		

	}
		
	
	

		

		else if(thing.term.degree < current.term.degree){

				
		previous.next=cast;
		

		cast.next=current;
		current=this.poly;
		current=current.next;
		

		return;

	}

		else{
			
			
		previous=current;
		
		current=current.next;
		

	}

}
		
		previous.next=cast;
	}	
	
	private boolean allZeros(Node head){
		Node current=head;
		
		while(current != null){
			if(current.term.degree!=0)
				return false;
			current=current.next;
		}

		
		
		return true;
	}
	
	private Polynomial deleteAllZeros(Polynomial p, int a){
		if(p.poly==null)
			return null;
		Node tmp=p.poly, prev=null;
		while(tmp!=null){
			if(tmp.term.coeff==0){
				if(prev==null)
					p.poly=tmp.next;
				else
					prev.next=tmp.next;
			
			}
			else
				prev=tmp;
			tmp=tmp.next;
		}
		
		return p;
	}
	/**
	 * Returns the polynomial obtained by multiplying the given polynomial p
	 * with this polynomial - DOES NOT change this polynomial
	 * 
	 * @param p Polynomial with which this polynomial is to be multiplied
	 * @return A new polynomial which is the product of this polynomial and p.
	 */
	public Polynomial multiply(Polynomial p) {
		Polynomial product=new Polynomial();
		if(p.poly==null)
			return null;
		else if(this.poly==null)
			return null;
		Node tmp=poly;
		Node tmp2=p.poly;
		
		while(tmp!=null){
			product=product.add(nodeMultiply(tmp,tmp2));
			tmp2=tmp2.next;
			if(tmp2==null){
				tmp=tmp.next;
				tmp2=p.poly;
			}
		}
		return product;
		
	
	}
	
	private Polynomial nodeMultiply(Node a, Node b){
		Polynomial nodeProduct=new Polynomial();
		if(a==null || b==null)
			return null;
		Node product=new Node(a.term.coeff*b.term.coeff, a.term.degree+b.term.degree,null);
		nodeProduct.poly=product;
		
		return nodeProduct;
	}
	
	/**
	 * Evaluates this polynomial at the given value of x
	 * 
	 * @param x Value at which this polynomial is to be evaluated
	 * @return Value of this polynomial at x
	 */
	public float evaluate(float x) {
		if(poly==null)



			return 0;



				Node tmp=poly;



			float sum=0;



			while(tmp != null){



			sum+=tmp.term.coeff*Math.pow(x, tmp.term.degree);



			tmp=tmp.next;






			}



				return sum;

	}
	
	/* (non-Javadoc)
	 * @see java.lang.Object#toString()
	 */
	public String toString() {
		String retval;
		
		if (poly == null) {
			return "0";
		} else {
			retval = poly.term.toString();
			for (Node current = poly.next ;
			current != null ;
			current = current.next) {
				retval = current.term.toString() + " + " + retval;
			}
			return retval;
		}
	}
}
